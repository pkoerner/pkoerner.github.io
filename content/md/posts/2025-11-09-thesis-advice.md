{:title "How to Write a Thesis: Things to Consider and Avoid"
 :layout :post
 :toc true
 :tags  ["thesis" "experience report"]}

Update 27.03.2026: Since I wrote the post, dgelessus provided some feedback I think is useful.
After many months, I actually incorporate it.
I will paraphrase the comments, clearly mark them, maybe add briefly to that.

During my time at the HHU,
I have published around 30 peer-reviewed articles,
advised around 25 bachelor's and master's thesis
and co-lectured a bachelor's seminar and graded the resulting essays.
There are many things you can do wrong in your thesis.
In this post, I compile some advice for your work.

Many things will seem obvious.
You will be surprised of (a) how many students did not follow obvious things, and
(b) how many obvious things *you* will not follow.

No thesis will be perfect. But there are theses which make plenty of writing errors,
and others that do fewer.
You can really level-up your writing if you "just" follow my advice.

The proper way to read this document is (a) to read it *before* you start your thesis (not "the writing phase"!),
and (b) to take notes while reading.
It is not some encyclopedia that you will refer to during the writing stage.
Write down things that seem sensible to you,
keep them on your desk or add a post-it to your laptop,
and re-consider that regularly. Maybe daily at first, and weekly later.
You have to be disciplined and follow this over months, or it will fail.
There is no "ah, I got it". You will need to remind yourself of most of the stuff, quite often.



# Disclaimer and caveats

This is the section you should definitely read first and reconsider for all uncertainties.

## Who is this document for?

The advice I give is primarily for computer science (CS) students,
and primarily for those in Germany.
Rules change once you alter the subject or the geographic location.

Students of the humanities, for example, might be given strict rules for formatting, citation style, etc.
In CS, just follow the LaTeX template that is given to you and you'll be mostly fine.
This means, you have less to worry about (or so it seems, we will revisit this point later).

Geographic region usually has less of an impact. 
Good theses from other countries that I have seen online still follow these guidelines.
However, expectations sometimes differ a bit.

## Just do this?

This is *not* a do-this instruction list.
Many questions that are often asked during the writing process do not have a definitive _yes_ or _no_ answer.
Moreover, so many issues lie in the "it depends" zone.
Let me give some examples for this:

### Should I write my thesis in German or in English? 

It depends!

- Do you feel comfortable writing in English?
- Will the text rely on English vocabulary anyway?
- Is it a topic worthy of an international publication?
- ...

In case you write in German, please do not overdo it. I have read the word "Streuwerttabelle" in a thesis.
I had to look up that they meant a hash map. It was weird.

Writing in English might be an advantage. 
It helps to formulate your text more precisely and technically if your vocabulary is limited.
It happens more often that you add useless asides, fancy adjectives and filler words if you know them.
But you do not need them.

### Am I supposed to use American or British English?

Listen, no one really cares. It's personal preference. Stop.


### Is it okay to say "I" in my thesis? Should I use "we" though I am only one person? Should I say "the author" or use a passive form? Help!

It depends!

Ultimately, this is a stylistic decision. I cannot make this for you.
In my opinion, nobody cares. But that's, like, my opinion, man.

Find out whether your advisor cares. If they do not, pick any one and simply be consistent.

### Should I put a related work section early on (e.g., section 2) or later (e.g., the second to last section)?

It depends!

In my opinion, put it in front if you rely on established techniques or if you extend them.
Put them later if it is just something similar you encountered.

I have seen great articles that even contain two related work sections, one early on and one later.

[dgelessus: You seem to want to say: Put it where it makes sense.]
Basically, this is correct, but hard to describe *where* it makes sense.


## Freedom

A thesis is a form of an exam. Note: it is the *freest* form of the exam.
Unlike a written exam, there is no rigid checklist what the expected answer must contain.
Unlike an oral exam, there is no way to ask for clarification while reading the text.

This is a blessing and a curse:
You are allowed to go your own way, *where appropriate*.
On the other side, there is no strict guideline "just do this and you'll be fine".

But not all is lost! There are basically patterns you can follow and others that you should avoid.
Will following the patterns make it the greatest text ever?
Probably not. But likely, it will be pretty good.
Will ignoring the patterns and freestyling it result in the greatest text ever?
Most likely not. Though: you might be the unicorn that finds a great way.

The risk-to-reward ratio tells me: 
Stick to the roads well travelled, and you might end up in a good place.
Or, as Dan John quotes Coach Maughan: "Be reasonable: Do it my way."


# Do: Keep meticulous notes

One weird tip I got was to write the article before doing the actual research.
I never really did this myself, yet I see the value of it.
What I did was that I have written down what I have researched, how I understood it,
enriched with my own examples, etc.

You do not have to lean towards an extreme on this.
But understand that many theses authors make one mistake:
They start writing the actual theses way too late because programming is way more fun.
Don't be like that.

As a first step to getting the point, check your ego at the door.
Most likely, you are a human that has some flaws. That's okay. Most of us are.
The thing is, we do usually not have a perfect memory.
Most of us cannot turn a great thought bubble into a 15 to 80 pages text on demand,
in a few days before the deadline.
So don't try. Write early what you can.

[dgelessus: I found it to be helpful to add notes directly to the LaTeX project in which I write the thesis later on.
This also helps with "I'm sitting in front of an empty page and do not know where to start."
You can also add notes as LaTeX comments so you do not have to worry about syntax and have a clear division between notes and proper text.]
Good call. Still I want to emphasize that it is more important *that* you note down stuff than *where* you write it down.

[dgelessus: Related: As soon as possible, create a git repository and actually commit and push regularly. Even the notes.]
If you do not see the why, please re-consider your career as a computer scientist.



## Benefits

The benefits of early writing are so obvious I almost did not put them in.
But please, consider this very strongly.

- *Life happens.* You might be taken out of your workflow for a few days.
May it be family, relationships, vacation, getting ill, having a day where you do not want to see anything of it at all, etc.
If you have your notes with you, you can look at where you were, get the full picture quickly and are back in no time.
Without notes, uhm, what did I do? What was I going to do? How does this work exactly?
- *Words produce more words.* When you have written down something, even it is just shorthand notes that do not form real sentences,
it is way easier to turn this into a text. It is easier to add something to that which might be missing.
It is easier to note that you have to explain something foundational beforehand.
It is easier to keep track of things that you cannot properly name and need more research.
Once there is *something* in your document, you can turn that something into *something better*
and keep refining.
Starting from blank always is hard.
- *Editing is easier than writing.* This is strongly related to the prior point.
Moving stuff around, polishing it a bit, removing typos, cleaning up figures; this is work where you can basically turn off your brain.
Organzising thoughts in your brain and getting creative to write a text is something you need to be in a mood for. You cannot easily do this tired.
- *Your mind is fresh from the task.* You implemented a tricky algorithm, designed a nifty data structure,
tracked down crazy bugs, made fancy optimisations or simply read some paper?
Now is the time to write it down.
Again, this does not have to be a "perfect text" - just put some bullet points in a text file and enrich it where needed.
The actually *writing* will happen later, when you do not have hours of coding behind you already.
But consider: Months from now, you will struggle to get the details correctly.
You will have to work again to understand it, or you will produce a crappy, superficial summary which might be wrong.
Keep in mind you do not have to use every single word you write down at this stage.
Feel free to delete (or, as we do, comment out) overly detailed points or even entire sections later on.

Now I have hopefully convinced you that it is beneficial to write stuff early on.
Next, find some guidelines on *what* you should consider writing down.

## Note down what you understand

You worked through a related paper and understood something new?
Write it down. Best, write it down *as you understand it*.
Maybe you need to refine it later on as you understood it better.
Add examples. Anything that helps you understand it later at a quick glance will help you.

Again, *maybe* you are not going to need it. Maybe you will subtract heavily from it.
But maybe it will be something that is important in a background section and you will be glad
(a) to have it written down already for your thesis, but mostly 
(b) you will be happy to have it as material for yourself to refer to later on.


## Note down what you did and will likely stay

You wrote some code or did some experiments? Cool!
Now is the time to write it down - if you are confident it will remain in your software.
Do not bother to precisely write down things that are very likely to change.
Feel free to keep rough notes of it, but also keep track of the concerns that you have.
This will help to keep track of trade-offs you might have made.


## Note down what you did and that gets thrown away for a reason

You did something and figured out that this is not the way?
*Commit it, then trash it*. That's fine.
Why should you commit it? So you can refer to it later on.
Why did it not work? I can show you!

What you did was an experiment. You drew your conclusions.
Keep track of that both in your repository and 
report it and your conclusions in your thesis. 
Keep track of the hash of the commit, maybe even tag it. Keep it on a branch if you have to.
Again, at least for now. Maybe it will be the least interesting thing later on.

This is something I too struggle with sometimes.
I did this and it was obvious trash from what I saw.
But arguing later on that it does not work, or is worse in any way?
Yeah, I did that, *I was there*, believe me!
But you can easily turn a nice anecdote into actual data with evidence if you follow this simple trick.


## Note down EVERYTHING you see

Again, quoting Dan John quoting Coach Maughan: "Make yourself a slave to good habits."
This is the most important thing here, and you have to exhibit the best discipline to succeed on this.

Keep notes and links to *everything* you see related to your thesis,
such as papers you read, web sites, blogposts or videos.
Download it and put it somewhere safe; sometimes information "disappears" or you just do not find it later.
Annotate the references with stuff you found interesting, topics they discuss,
sentences that stuck out to you, conclusions that might end up important.

Nothing is more frustrating than remembering "I know I read it _somewhere_".
But finding that again? Good luck!
This will also help filling up your background and related work sections.
Your document is almost empty two weeks into your thesis?
Do your darn research already!

[dgelessus: If your source already offers a BibTeX fragment, copy it directly into your .bib file.
If you take notes in your .tex, directly add a citation.]

# Structuring your thesis

Please, please, please put some thoughts into the structure of a text.
Yes, some things are basically fixed and will look like this,
and straying too far from this template will be objectively wrong.

- Abstract
- Introduction
- Background [& Related Work]
- Your Main Part
- [Experiments]
- Results
- [Related Work]
- Conclusions & Future Work

But here's the deal: *Each of this sections will have to be structured*.
Students tend to make two mistakes in putting down as much information as possible somewhere.
The first mistake is having too much information; we will return to this later on.
The other is the *somewhere*. I have often heard "but I wrote it down!".
Where did you put that piece of crucial information? Where I needed it when reading, or some later section?

I mostly read a thesis from start to finish. Don't make me jump from section to section and back again.
But if you absolutely have to do so, at least tell me that you are going to discuss it later on.
In the paragraph above, I just did that: "The first mistake is having too much information; we will return to this later on."
Best, put a reference in your LaTeX.


## Do: Make your structure obvious

So you wrote down your stuff. That's great. Now we enter the editing phase.

Make use of everything you can to structure your text.
You can add additional sections, you have subsections at your disposal,
you have subsubsections, you can use paragraphs, when in doubt, you can add your own formatting.
You can use itemizations or enumerations where appropriate.
Break paragraphs with double newlines to separate different thoughts from each other.
Just do this.

Then, check your structure. Does it make sense? Is it a random order?
Is everything you refer to explained beforehand?
Likely, you will have to move stuff around. That is fine.
It never is perfect on the first attempt.

Do you have a section heading directly in front of a subsection heading?
A subsection heading in front of a collection of paragraph?
That is a bad sign.
Explain what is going to happen in this section, in correct order.
Put these two sentences between the headings.
Check again: Does this make sense to you? Is clarification needed?

There are many variations of a famous quote of which the source seems to be unknown.
"Tell 'em what you're going to tell 'em. Then tell 'em. Then tell 'em what you told them."
This makes your structure obvious and give you the opportunity to check whether it works.
If it does not, it is time for a change.

This pattern - overview, content, reflection - works on different "zoom levels" of the thesis.
The thesis itself follows it: Introduction, main section, conclusions.
Make every section follow this pattern, maybe even on subsection or paragraph level.
If something is important, repeat it at the end.
If it sets the scene for the next big thing, state it and use that as your transition to the next section -
which in turn explains what you have seen and how it relates to the next stuff.


## Don't: Let generative AI take care of your work

I include this point here, because this is something that generative AI loves to do.
It gives short paragraphs, it highlights points visually, it states key words or key phrases
for each thought.
This is great overall!

The issue is that generative AI does this in a very unnatural way.
It overdoes it. And the worst thing: It is trained to be *convincing at a glance*,
not to precisely convey information.
What may seem like a good text at first glance will not withstand
critical inspection.
There will be lots of hollow phrases.
Trust me: Expert-level readers *will* pick up on that and will be put off and disgusted.

Avoid this at all costs and do this yourself, for the love of all that is holy to you.


# Do: Make clear your motivation and task

This is an error that stems from writing too late.
Your introduction has to clearly state the context, the motivation and what this entire thing you are doing is about.
The worst thing: It has to be understandable for (a) someone who is not you (!)
and (b) someone that did not put months of effort doing what you did.
Basically, someone that was you before you started the thesis.

Take a couple of pages to make this *very* clear.
The rest of your thesis might not make sense to the reader if they do not understand what you are doing from the start.
Give examples that motivate your work early on.
Relate it to something that is widely known.
Have you heard of it before you started your thesis? No?
Likely, this is too specific already to properly introduce your topic.

This might be the most bang for your time issue to tackle.
Once you set me up properly with the correct idea in my mind,
I will have an easier time to follow you through the rest of the paper.
At the very least, do not make me feel stupid for not knowing what is going on.

An easy technique is "zooming in" from the very outside. As a very abridged example:
Today, software is everywhere. (That makes sense.) 
Software is known to have bugs. (Yeah, I have seen that!)
One technique to locate bugs is static code analysis (either: I know that, or: huh?),
where the source code is considered without executing it with concrete values (either: I know that, and I agree, or: okay, I have some kind of idea).
A specific analysis in lower-level programming languages like C is use-after-free (either: I know that, or: what is that?),
where one attempts to locate instances of pointer dereferences to memory locations that are already freed (hopefully: ah!).
An example of such code is given in Listing X. ...
The goal of this thesis is to improve precision as well as performence of this analysis.

Note that each of the points tightens the scope a bit:
From software overall, to code quality, to static code analysis, to use-after-free analysis.
I imagine everyone in CS has heard of code quality.
But (sadly) not everyone knows static code analysis tools,
or has written some.
Not everyone knows about memory management. 
Here, you can add first explanations.

You can (with experience easily) stretch this to a page already.
Each of the sentences only contains the very essence of that thought,
and they just claim things.
You can give evidence for such claims, right?
Give it a bit of flavour text.
It does not have to be very precise at this stage,
instead focus on not losing anyone in this section.


# Do: Make your points almost too obvious

A thing to consider is that you fought with the topics you wrote about for months.
You (hopefully) know the ins and outs of what you did.
This is a blessing and a curse.
The blessing is: It all makes sense to you.
The curse is: It does not make sense to anyone else, and you cannot see it.

For every point you make, for every implementation detail you present,
consider writing down (a) why you think this is interesting,
(b) why it matters and (c) what you are getting at.
This does not have to be a lot of text and might be a short sentence.
Just make it obvious. Too obvious for you, maybe - that translates to "barely understandable with some work" for everyone else.

You will see that this essay has some repetitions, goes on longer with the same idea and offers several ideas
that are very close to each other. This is the point.
I hope you will understand and take away at least one instance of the many times I mention something.


# Don't: Dive into details too deeply too fast

This is related to several points above.

Give the reader time to acclimate: Give an introduction at the smaller level.
Review the structure. Give examples to illustrate what you are doing.
Add figures where appropriate.

If you jump straight into technical, complicated stuff, you *will* lose the reader.
Again, don't make me feel stupid for not understanding your explanation.
Keep it simple, explain something like you would on a whiteboard,
go through the steps, give the reader an opportunity to check whether they understood it.

The more complicated the matter it is, the more layers you should add.
Give a rough intuition what happens, why it is needed, what the result is.
Then, add details. Only afterwards include all the dirty stuff, if necessary at all.


## Don't: Overly explain basics in the background section

What should your background section consist of? This is very much an _it depends_ answer.
There are, however, things to look out for.
Below, I assume that you are writing a thesis at the STUPS group at HHU.
We work a lot with B and Prolog, and I taught Clojure there.
Of course, other research groups have other "obvious" things,
and things we deem "obvious" might be new and worth of explanation for other groups.

As an example: If I want to introduce the B method in the background section,
I should, for example, talk about the purpose of the method and what a B machine specification file looks like.
After that? It depends. Should I talk about machine refinement, proof obligations and proving tools?
*Only if it makes sense for the contents of my thesis.*
Do I touch refinement at all? No? Don't talk much about it then; a sentence at most.
Is it essential for my thesis' topic?
Give more than two paragraphs of information, this stuff is complicated after all.

Let's consider other things:
Should I introduce Clojure because I used it as a programming language?
That is hardly a good reason.
Does the language have interesting features I rely upon?
Is Clojure's macro system relevant?
If so, quickly introduce it and add a quick explanation.
Otherwise, drop it.

Am I working on a code analysis of Prolog?
It might make sense to describe facts, rules and clauses.
Should I explain the execution model in detail?
Probably should stick to a quick, simplified explanation.

The more you talk about something, the more it should be relevant for the further contents.
Also consider: The more you talk about something, you might add statements
that an expert might consider debatable or plain wrong.
This is where you do not want to end up.

Many theses included, for example, a bad introduction to B or Prolog, seemingly for no reason.
Keep it short, but make sure you explain everything you rely upon on your thesis.


# Don't: More is just more

Some students are scared they may not have enough content to come even close to the page goal of the thesis.
This, again, is induced by starting to write way too late.
If you keep plenty of notes, you have a good overview of points to elaborate.
If you formulate them into text early on, you will have a good feeling of your progress.
Indeed, contrary to their initial fears, many students end up having to shorten their texts.

When you do not have any idea what your contents might be (because you sit before an empty page),
you tend to be overly wordy.
You add filler words, you desperately search to fill the pages, you add information that nobody cares about
and every hope for a useful text goes overboard.
On the other hand, if you write your text knowing you have plenty of time left,
you remain precise.

Just because you have more text, the result is not necessarily gets better.
Check regularly whether all information is necessary,
remove sentences that are uncalled for and trade length for clarity.
This is hard, but it pays off.


## Don't: Stream of information

Watch out for sections that just go on and on and on, packed with content.
If you do not back off from giving details, if you do not return to the reflection stage
and introduction of a new concept, you are likely doing something wrong.
Probably, you need to structure your contents better.

Some students do not keep their focus on a single point.
Instead, they jump from one topic to the next, to the next.
Again, this might be a structural error.
It is very hard for the reader to keep up, to locate what is really important
and to get a mental breather.
Don't make the reader _suffer_ through your text.
The more mental load you take off them by backing off, adding examples, etc.,
the more likely it is they understand _something_.

Often, it is better to include fewer details for the sake of being understood.
However, this is not always true.
If you are doing something that demands mathematical rigor, that includes a proof,
that requires a complete list of translation rules, you have to provide that in some way.
It can be sensible to give a common idea and group other information around that.


## Don't: Overly lengthy sections

This is very similar to the points above.
When a section just keeps going on,
you should probably structure it better.
Re-group your information, move it around,
and try to keep the chunks manageable.


# Do: Reference figures, code listings, line numbers

Pay attention to all information that you add for understanding.
One too common mistake is to add figures - and then not to reference them.
If you do not include them in your text, you are doing something wrong!

What about code listings or algorithms?
There is plenty I could say about that.
Try to keep them short. Rename variables or function names.
Get more pseudo-codey and group instructions together.
Do all the dirty tricks so I don't have to suffer through your code.

Does your code listing have a caption? You better reference it.
Does your code listing have line numbers?
You better make use of those and point to the lines that are most interesting.

Is your code snippet short and very important to consider *now* in the text?
Consider not wrapping it in a floating environment and inline it in the text.

# Don't: Make up your own vocabulary

You designed some architecture, implemented an algorithm, something like that.
You _made_ something. Thus, you get to name it. Right?

It depends (but no).
Vocabulary is very important for people to understand what you are doing, and also, what you are not doing.
Find out whether you re-discovered something that exists and has an established name.
If so, you do not get naming rights. Use that name instead.

Also, find out whether something similar exists.
Avoid using that exact name. Find out why it is named that way and what the exact differences are.
Then, and only then, maybe you are allowed to come up with a new concept name.
But don't go overboard; instead, keep it close to the original and only modify the parts of the term
in which the differences lie.
Maybe add another word to it to distinguish the concepts.

Many instances of such re-invented terms just scream "I did not do my research".

# Do: Consistently look out for related work

Speaking of doing your research:
This is not a phase you do for a week at the beginning of your thesis.
Keep re-iterating your searches at least once a week, maybe even more often.

You will be surprised how much you learn and how your way of thinking and naming can change.
Halfway into your thesis, you will search for entirely different terms and come up with
a lot of different publications.
As your understanding refines, you will be improve in linking related works to your thesis.
Keep doing that, and you will come up with a solid section on related work.


# Do: cite early, cite clearly, cite the proper thing

These are multiple things that I can't really get my head around how you can do it wrong.

First, there is the question of "where do I put my reference".
I do not see how you mention something three times and the fourth instance is where you put the citation.
Always add a citation at the first mention.
Maybe additionally put another were you discuss it in more detail.

Second, as an engineering science we are often not too concerned with direct quotes.
Often, we are happy with saying "X and Y discuss the value of Z and come to the conclusion that ... [Citation]".
That's fine. But rules change if you quote directly from a source, especially if translation from another language is involved.
Make sure that you mark the start of such a quote, and the end of it.

Consider the following:
"Some authors are of the opinion [Citation] that verbal translation. Another sentence of verbal translation. Now my opinion follows."

You cannot see where the content backed by your source ends, and where your opinion starts.
_Never_ do that. Always ensure that your content is clearly separated from your sources.
Add quotation marks or formatting where necessary.

Third, put some effort in locating the thing you want to cite.
I cannot stress it enough.
The ProB tool has *the* two papers, one a conference version and one a journal version.
The Rodin tool has *the* paper, the B method has *the* B-book (okay, the Schneider book exists too),
for Event-B, there is *the* book.
For Clojure, there is *the* publication.
To me, it is absolutely clear what *the* publications are for these and many other things.
It should be for many things you are considering. Just read the darn thing, or at least the abstract, introduction and conclusion.

[dgelessus: In some cases, unfortunately, it is not absolutely clear what the proper citation is.]
In my experience, such cases exist. But such instances are rare.
If you cannot positively identify *the* publication, ask your advisor for assistance;
or add your doubts to the text around the citation.

[dgelessus: Tool authors often offer one (or sometimes more) citations on their webpage that is preferred.
If they do, you should absolutely use that.]

And no, it is *not* okay to cite any paper that does something *with* ProB as a witness
for all the stuff ProB does; likewise, for the other tools.
I would be appalled if you cited my integration of B in Clojure when you introduce Clojure to someone.
And yet, I sometimes get notification my articles were cited by some _idiot_ that clearly did not understand anything related to the contents.
This immediately screams "low-effort pay-to-publish spam publication" to me.

[dgelessus: If you cite a statement from a publication, be careful whether this statement is a citation itself!
If it is, find the original source and verify that the original publication actually contains such a statement.
Otherwise, misinterpretations and wrong citations will propagate.]

If you find something that contains a good explanation that you like, cite it *additionally*. That's fine.
But don't make it your only source. Spend some effort to locate *the* publication.
Likely, it is already cited in that paper you found.


# Finalizing your thesis

So, we are getting near the end.
All the hard work is done, you finished your implementation (i.e., everything now is future work aka "not gonna do that"),
you ran your experiments, you wrote consistently (ha!) and the text is pretty much done.
Sure, there are some improvements you can make.

I encourage you to decide "this is not perfect but pretty good",
and pretty good is often good enough.
Yet, do the following cleanup steps at the very end.
Do not change *anything* else later on as you will suffer.

## Consider: Spell checking and grammar tools

It's so simple. Run a spell checker. I like using aspell with in-place editing.
I also like using the spellchecker integration in vim.
Yes, doing that combined with LaTeX sucks, especially if you make heavy use of TikZ and labels.
But you will manage, as you will only need one pass after all.

You can also use other tools that are freely available online.
LanguageTool can be called from vim and also has freer forks available.
Find something that fits your needs, no need to pay for it, and use it.

### Bonus tip: Splice figures and listings in a file each

So you created a nice tikzpicture? Great!
Just, do not put it into your main tex document.
Copy + paste it to some other file and avoid the spell and grammar checkers complaining every time.

Maybe you also want to force LaTeX to put a figure into a very specific place.
This sometimes only works by moving it in the text.
I prefer only moving an include instead of plenty of lines, so I can still see the context where it is placed in the tex.



## Consider: Minor LaTeX issues

There are a few things that are more LaTeX-specific that you can take care of quite easily.
Below, I will tell you about some.

### Renaming terms and using commands

Imagine having written your thesis.
But then you notice, someone did something similar already.
And as horrible as that person was, they named it differently than you did!

So, you want to make changes to that term. Have fun to locate all instances.
Search and replace can help, but maybe you have a typo sometimes, are have not been consistent
(do I write pre-condition or precondition? counter example, counter-example or counterexample? ...).
You have to use the thing between your ears for this:
If a term seems really important, and you use it regularly throughout your thesis,
you can often see it from far away. Develop an instinct for that.

Once you have identified such a term early on, you can use commands for it.
Provide an option for upper and lower case as well as singular and plural; so four commands overall.
Then, only use those in your text.
This (a) forces you to be consistent with your terms and (b) gives you the flexibility to change all instances
at once at the last minute.
Just make sure to terminate the command usages or set everything up properly - otherwise whitespaces might go missing sometimes
which is just the worst.

[dgelessus: My preferred solution for custom commands is to always call them explicitly with empty arguments,
i.e., `\bla{}` over `\bla`. This usually works.]
I vaguely remember that a package exists that forces termination somehow.
I do not know whether it actually does that, how it is named and whether it actually does this
or whether it accidentially worked for my problems.
Thus, I do not want to propose this as a solution.


### Widows and orphans

Lastly, we have something called "widows" and "orphans".
Basically, if you have a single last line of a paragraph that gets to live on the next page,
or a single first line that remains on the prior page, you have one of those.
This also holds true for itemization points, etc.
Nobody cares which is which (except maybe professional typesetters).
From a layouting point of view, they are horrible.
Take care not to have them in your final document.

There are some ways to cheat around that. Add a few filler words to prior paragraphs,
or shorten a sentence.
As a last resort, insert tactical pagebreaks or increase the page capacity with enlargethispage.
Once you have done this, there is no proper going back.
Adding a paragraph in the introduction changes *everything*.
This is why you take care of this last.

