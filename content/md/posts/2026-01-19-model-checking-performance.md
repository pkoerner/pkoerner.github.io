{:title "The Quest for Model Checking Performance"
 :layout :post
 :toc true
 :tags  ["reflection" "university"]}

# Preface

This is the start of a new series:
I want to share insights from my activities during my university time (2010-2025),
highlight results of my research and give a better idea of my skill set.

The main idea of posting each publication independently was to have room
to discuss key insights on the technical side and post a preprint version
(which requires some additional work to strictly adhere to the publishing agreements).

This series, however, aims to paint a larger picture by grouping together publications
that tell the same story.
This is not always clear to someone from the outside (and in many instances, even to my colleagues).
So, these posts are intended to strike a more casual tone.
I will explictly name leading co-authors and protect the innocent students whose theses I supervised.
I tell the stories to the best of my recollections, so inaccuracies might occur.
Sorry to anyone I forgot to credit!



# Introduction

Exhaustive model checking is quite time-consuming.
This is even more the case for B/Event-B and the [ProB](https://prob.hhu.de/) tool,
where (a) the model is interpreted and not compiled,
and (b) state transitions and properties (guard, invariants) can express the result of 
millions of low-level state changes.

To improve the performance, there are basically two approaches that always work:
- Throw more resources (CPUs) at the problem.
- Use cleverer algorithms.


# The Parallel / Distributed ProB Trilogy

ProB is implemented in SICStus Prolog.
Ironically, it started as one of the early, most parallel Prolog systems -
and now does not allow any threading whatsoever.

I experimented quite heavily with how to move the representation of B states (Prolog terms)
from one thread to another.
I learned much more about shared memory, page layouts, mutexes, etc. than I ever wished for.
First experiment were with the SICStus' Jasper interface (a bidirectional Prolog-Java system).
At least at the time, it was quite... a wild ride.
I ended up not chosing this technology.

Together with Jens Bendisposto - *the* Java guy at pretty much the entire CS department -
I tinkered on a prototype in C, making use of SICStus foreign function interface
and the [ZeroMQ](https://zeromq.org/) messaging queue (I still quote from its guide sometimes).
Jens hated C with a passion (it is not garbage collected!).
I just self-learned it for the project of the computer architecture course.
Surely, I was young, naive and eager to put my new skills to work.
Boy, [did I not know what I didn't know](https://en.wikipedia.org/wiki/There_are_unknown_unknowns).

As my bachelor's thesis, I vastly improved our little prototype.
I implemented a mutable shared-memory version of Bagwell's [hash-array mapped trie](https://en.wikipedia.org/wiki/Hash_array_mapped_trie)
to store seen program states without replicating them 20 times.
I learned that this is the very data structure that underlies Clojure's maps, vectors and sets.
(Funny how that happens.)
We ran it on AWS for a bit and had happy dreams about model-checking-as-a-service.
Later, I even supervised a bachelor's thesis for a dedicated cloud controller.
My thesis work was a huge success, offering many great features implemented in the most horrible
junior-level C code you would have seen.

After my thesis, I re-wrote the damn thing,
trading feature-completeness for simplicity and stability.
I ran it at the university's high-performance cluster
and got a >400x speed-up with 500 cores with almost linear scaling.
That is *pretty* good.
At this point, we the boundary was more that
we did not have models that were large enough to scale further
yet were still of finite size.
So, overall, I deem it a successful project.


## The One(s) Who Got Away

I never got around to make the shared-memory implementation lock-free.
There is a [great paper](https://arxiv.org/pdf/1709.06056) on the topic,
but it assumes the shared memory is garbage-collected.
I think with the constraints we have in this setting (a known number of worker threads
and insertion-only), it could be tweaked accordingly.


# The LTSmin trilogy

After my work on my bachelor's thesis, there was some conspiring going on
between the adults (i.e., doctorates, post-docs and the professor).
Some ideas were carefully discussed out of my earshot.
After a while, there was a request for my work:
Another C extension of ProB was required in order to wire ProB up with [LTSmin](https://github.com/utwente-fmt/ltsmin).

I was kept in the dark about the details at this point.
I understood that LTSmin was another model checking tool,
that it had advanced model checking algorithms and
shall use the ProB interpreter to model check B.
Later, I learned that the interesting features were:

- symbolic model checking using decision diagrams (BDDs/LDDs)
- a multi-core backend
- a partial order reduction (POR) based on stubborn sets.

ProB at the time had an implementation of POR using ample sets,
implemented by Ivaylo Dobrikov for his doctoral thesis
(he ended up teaching me most I know about POR).
The implementation of LTSmin was proven to work highly effective,
yet ProB's was not.

So I implemented the communication based on the interface I was explained.
We wrote a [nice article](/posts-output/2016-03-15-iFM16-ltsmin-prob) on that
(which - at the time - I actually understood little of).

As it turns out, much of LTSmin's potential remained locked,
as ProB did not provide enough information.
There was more work to do, I needed a topic for a master's thesis,
so Jens Bendisposto and Michael Leuschel took me to Enschede.
At the University of Twente, we discussed with Jeroen Meijer and Jaco van de Pol
what could be achieved and how it works in detail.

[So, I implemented that](/posts-output/2018-06-29-iFM18-ltsmin-prob).
There were some surprising results:
LTSmin using ProB was faster than ProB when doing the same thing as ProB.
This inspired [huge improvements in ProB](https://doi.org/10.1007/978-3-031-07727-2_8) that Michael Leuschel implemented later.
And: LTSmin's POR implementation is not much more successful than ProB's.
This inspired me to re-visit POR for B.


## The One(s) Who Got Away

One of the initial visions of the LTSmin integration
was to provide tooling for the CSP||B formalism,
where a CSP specification controls a B machine.
The idea is that program flow is easier to describe in the process algebra CSP,
but state transitions can be better described in B.
So, a CSP specification limits how a more non-deterministic B model may act.

While we implemented a very rough version of this,
many improvements could be done on the CSP part (which would have been the third part of the trilogy).
The main issue was that the CSP interpreter was... let's say, a bit dated
and it did not receive much love.
Later, I supervised a student that re-wrote huge parts of the CSP interpreter as his master's thesis.
Yet, nobody touched it ever again (as the group interested in CSP||B was geographically too far away to complain).


# The Partial Order Reduction Dream

As mentioned above, the LTSmin integration gave us an interesting data point:
*It is not the implementation* that hinders successful partial order reduction.
Moreover, it is something with B models and their analysis!

From the data I gathered, the most important thing here is the abstraction level.
As explained in the introduction, in B, you can express millions of low-level state changes
in one single operation call.
But, the analysis in ProB (whose results are passed to LTSmin) does two important things wrong
(careful, things get technical here):

1. Operations are considered individual at their top-level.
This means: if you have a `foo(left)` and a `foo(right)`
it is the same operation; thus, it cannot commute with itself.
Lesson learned: The parameters must be considered to be part of the operation!
2. Variables are considered to be the same, even when they are compound values.
If you have an array-like structure (sequence) `[1,2]`,
the first slot cannot be treated independent from the second slot.
So, if you group together information that could be acted upon independently
(like, which blocks are reserved per train route),
you are in trouble!

The second point *can* be found, but it requires costly constraint solving
(usually, one quickly approximate things with a purely syntactical analysis based on what variables are read from and written to).
And once you analyse all combination of operations,
the analysis phase might become longer than the model checking process of the original model.

If you re-write models in a more POR-friendly way (which we call "data refinement"), things change.
The model becomes (a bit) lower-level and less abstract - but the POR can work on that.
This is the main result published [here](/posts-output/2022-05-06-VSTTE22-por).


## The One(s) Who Got Away


Jan Roßbach implemented [a tool](https://github.com/JanRossbach/fset) using lisb in order to automatically
the data transformations I described above. I used this for my experiments to test my hypothesis.
This is a good start, but I am convinced we can do better:

- We can improve automatic data refinement if we understood better what patterns are prevalent that hinder POR.
- The implementation of POR should consider parameter values and treat slots of compound values independently.
- There might be other information that is useful. For example, if certain actions have a fixed ordering
  (for example, reserving a route, set the points on the track, letting the train pass, freeing the track),
  we can use this for more precise analysis.

I am convinced that there is much work that can be done to bring the POR implementation to a usable state for B.
Thus, I was very shocked when Michael Leuschel loudly thought about removing it from ProB,
as it rarely yields any benefit.
On the other hand, the necessary work would at least require another doctoral thesis.



# The ProB VM Idea

A third idea was more specific to and aimed at changing the representation of the constraints.
At its core, ProB is implemented in Prolog. It is easy to write AST interpreters in this language.
Thus, an open question was whether a bytecode-level interpeter would perform better
than an AST-interpreter in Prolog.
To the best of my recollection, the idea was pitched by David Schneider, at least to me.
I am not aware of prior discussions between "the adults".

Half of my master's project was to experiment with it.
And, despite all efforts, the answer is, quite surprisingly, no.
See [the paper](/posts-output/2020-12-01-WFLP20-bytecode-interpreters-prolog) for details.


# Code Generation

In the introduction I stated that ProB has an interpreter for B models.
In particular, it does not execute compiled code.
Fabian Vu [changed the rules somewhat](/posts-output/2019-10-01-iFM19-b2program)
based on an idea by Dominik Hansen.

If you refine B models enough, so that almost all abstraction (functions, set variables, etc.) is eliminated
and replaced by implementation details,
code generators can be applied to obtain code that can run on embedded devices.
But for many instances, we are happy to provide a run-time with heap allocation, etc.
if that means we can execute the model faster.

There are some trade-offs here.
Mostly, some rules have to be followed; some refinement must still occur;
and unbounded enumeration may easily happen.

I was more in an advising position based on my knowledge of B, compiler construction
and immutable, yet high-performing data structures.
I will not claim much credit to Fabian's excellent work as I was pulled into the project
somewhat by accident.


