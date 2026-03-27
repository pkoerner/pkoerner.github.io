{:title "The Art of Code Listings"
 :layout :post
 :toc true
 :tags  ["thesis" "experience report"]}

One of the things that go wrong in theses are, surprisingly, code listings.
In this post, I will focus on this topic, identify many bad patterns
and try to convince you to do better.


# Don't: Here's Code I Wrote!

One of the worst offenders is the following thought:
"This piece of code is important. It must be shown in the thesis!"
So, you copy and paste the code as-is, verbatim.
As you, as the writer, know exactly what you mean,
you then prompty forget to explain what the heck is going on.

I give you an example for this.
It is, on purpose, a large snippet of C code.
Next, it uses the awesome ZMQ library which I assume you are not familiar with,
just to emphasize the point.
Lastly, it is not even great code.

```
 1 zpoller_t *poller_pull = zpoller_new(pull, NULL);
 2 zpoller_t *poller_rep  = zpoller_new(rep, NULL);
 3 
 4 int work_sender_active = 1;
 5 zlist_t *hash_accumulator = zlist_new();
 6 int64_t last_time = zclock_mono();
 7 while (!zsys_interrupted) {
 8     if (zpoller_wait(poller_pull, 1)) { // it is okay to poll on this one for a while
 9         int rc = master_h_pull(pull, pub_cmds, pub_hashes, strict_mode, &stats, &proxy_ips, fd_logfile, &wqs, max_states, trie, msg_log, hash_accumulator);
10         if (rc == -1) {
11             break;
12         }
13     }
14     if (zpoller_wait(poller_rep, 0)) {
15         master_h_id(rep, master_ip, PORT_PUB_HASHES, &proxy_ips, model, 1, trie);
16     }
17 
18     if (work_sender_active) {
19         work_sender_active = work_sender_no_loop(&stats, &proxy_ips, q, fd_logfile);
20     }
21     int64_t tmp = zclock_mono();
22     if (tmp - last_time >= hash_cycle_msecs) {
23         if (zlist_size(hash_accumulator)) {
24             send_hashes(pub_hashes, hash_accumulator, fd_logfile);
25         }
26         last_time = tmp;
27     }
28 }
29 dprintf(fd_logfile, "[DEBUG] quit main loop\n");
30 fflush(NULL);
31 send_hashes(pub_hashes, hash_accumulator, fd_logfile);
32 
33 dprintf(fd_logfile, "[DEBUG] sent hashes\n");
34 fflush(NULL);
35 zlist_destroy(&hash_accumulator);
36 
37 puts("done");
38 puts("blocking until all messages are processed by proxy...");
39 dprintf(fd_logfile, "[DEBUG] checked: %ld, known: %ld\n", trie_get_checked_states_count(trie), trie_count_elements(trie));
40 fflush(NULL);
41 
42 while (!safe_to_terminate(max_states, trie_get_checked_states_count(trie), trie_count_elements(trie))) {
43     // take care of dangling hash messages etc.
44     if (zpoller_wait(poller_pull, 1)) {
45         int header;
46         zmsg_t *msg;
47         int rc = zsock_recv(pull, "im", &header, &msg);
48         assert(rc == 0);
49         dprintf(fd_logfile, "[DEBUG] checked: %ld, known: %ld\n", trie_get_checked_states_count(trie), trie_count_elements(trie));
50         zmsg_print(msg);
51         fflush(NULL);
52         if (header == P_IS_HASH_MSG) {
53             rc = zsock_send(pub_hashes, "im", CTRL_ADD_HASHES, msg);
54             assert(rc == 0);
55         } else if (header == P_RESULT_MSG) {
56             zmsg_print(msg);
57         }
58 
59     }
60 }
61 shutdown_everything(pub_cmds);
```

The accompanying text often looks similar to this:

> The main loop of the leader process is very important, as it runs until it does not.
> Afterwards, it waits until termination is safe and terminates afterwards.
> This is shown in [the code listing].


# The Problems

Oh. My. God. This is horrible and I felt disgusted at myself for pasting all that.
Why? Many reasons.


## The Text

The text that references the code listing contains exactly two pieces of information:

1. Why does the code exist (in the code base)?
2. The code in the listing is related to the rough idea.

But, it does not explain what I am looking at.
Why are you showing me the code?
What are the intersting bits?
What the heck even is going on?

I often argue that you should use line numbers, both next to you listing and in the accompanying description.
Let's try it out:

> The leader process is shown in [the code listing].
> The main loop (ll. 7-28) is very important, as it runs until it does not.
> Afterwards, it waits until termination is safe (ll. 42-60) and terminates afterwards (l. 61).

Looking at the text now, you can see that you have three ideas in the code:
A main loop, waiting for termination, and terminating.
That's it - unless you further describe it.
But the question remains:
Why are you showing me all this then?




## The Code

Next, let's look at the code listing itself.

### Noise

This is advice that always holds true.
Yet, in some programming languages it is more prevalent than in others.

Let us look at some of the many examples above:

```
37 puts("done");
38 puts("blocking until all messages are processed by proxy...");
39 dprintf(fd_logfile, "[DEBUG] checked: %ld, known: %ld\n", trie_get_checked_states_count(trie), trie_count_elements(trie));
40 fflush(NULL);
```

Here, we see debug printing and progress reporting in action.
This is important to have in a code base, for sure.
But, unless you are talking about *your fancy debugging and progress reporting mechanism*,
this is just noise. Delete it.

```
53             rc = zsock_send(pub_hashes, "im", CTRL_ADD_HASHES, msg);
54             assert(rc == 0);
```

This is an assertion checking that the return code (rc) indicates no error occured during sending.
Again, this is good to have in the code base,
but unless you are talking about issues why message sending might fail,
this is not interesting.

```
35 zlist_destroy(&hash_accumulator);
```

Allocation and freeing usually is boring.
If there is no point in showing off a clever system,
try to get rid of it as much as possible.


### Missing Abstraction

Now, let us consider implementation details on this example:

```
21     int64_t tmp = zclock_mono();
22     if (tmp - last_time >= hash_cycle_msecs) {
23         if (zlist_size(hash_accumulator)) {
24             send_hashes(pub_hashes, hash_accumulator, fd_logfile);
25         }
26         last_time = tmp;
27     }
```

First, `zclock_mono()` is a library function.  What does it do?
Do you care to elaborate, or are you expecting the reader to check out the documentation?
That are all these fancy variables, like `hash_cycle_msecs`, `pub_hashes`, or `fd_logfile`?
Sure, I can *guess*, but this does not bring any benefit.

You have two options here:
Either, this is something interesting that you want to explain in detail.
This could be something like:

> Because it is more efficient to bundle the hashes, we do not send them on every iteration.
> Instead, we use a fixed-time interval (`hash_cycle_msecs`) that is configurable at startup.
> Only when this interval elapses (l. 22), we publish the received hash codes (l. 24) and reset the timer (l. 26).

Door number two is, this is not interesting at the current level you are talking about.
This is most likely the case if your snippet is longer than 10 lines. Seriously.
Instead, create an *abstraction* for the code that is easier to comprehend.
This could look like:

```
21 if (timer_elapsed(hash_cycle)) {
22    publish_hashes(hash_accumulator);
23 }
```

Or, maybe even:

```
21 // publish hashes if timer elapsed
```

Much easier to read and less brain power required to what you are talking about.

# Putting It All Together

Now, let's add proper abstraction.
Note that many unexplained variables disappear,
new comments might appear,
the code becomes more compact, more pseudo-code-like and is easy to digest.

```
 1 zlist_t *hash_accumulator = zlist_new();
 2 while (!zsys_interrupted) { // no CTRL+C
 3     if (zpoller_wait(poller_pull, 1)) {
 4         done = receive_messages(pull);
 5         if (done) {
 6             break;
 7         }
 8     }
 9     handle_registrations_if_any();
10     distribute_work_if_any();
11     if (timer_elapsed(hash_cycle)) {
12         publish_hashes(hash_accumulator); // resets the accumulator
13     }
14 }
15 
16 while (!safe_to_terminate()) {
17     receive_hashes(pull);
18     publish_hashes();
19 }
20 send_termination_signal();
```

Next, let's fix the text.
We assume that all detail that remain is necessary.
Thus, we have to talk about it.

> [The listing above] shows how the leader process operates.
> The main loop (ll. 2-14) runs until the process is interrupted via SIGINT (Ctrl+C),
> or until the received status messages indicate that no more work is to be distributed (ll. 4-7).
>
> The two other responsibilities is to accept new worker processes 
> (l. 9), as they can be added dynamically while the process is running),
> and to distribute work items that the process started with (l. 10).
>
> In order to reduce network stress, information about processed work items
> is published not in every iteration but only after a configurable timer elapses.
>
> The main loop is an custom implementation of the reactor pattern.
> It does not use the `zreactor` class, as it would poll at least one millisecond
> on each socket per task.
> As only receiving hashes is time-critical, we only allow polling on this socket for some time (l. 3).
> This also avoids busy-looping and reduces CPU stress.
>
> When all queues are empty, it might not be safe to terminate the process as some results might still be in transit.
> Thus, we have to wait until we can be sure that all items are processed and the information is received (ll. 16-19).
> As the leader process does not maintain this state itself, the information has to be published to the procy process (l. 18).
> Only when it is deemed safe to terminate, the signal is given to the other processes (l. 20).

Now, we actually talk about the stuff that happens, why it is designed this way,
why alternatives were discarded, what the benefits are, etc.
We actually found something that might be interesting to talk about!


# Summary

As always, this guide is not a set of "do this" guidelines.
It should give you a rough idea of things that are bad, and how you can resolve them.

The first version I gave you was horrible and a pain to go through.
The text did not add sensible information.
With only a couple tactics (and, admittedly, some experience),
we are able to turn 60 lines of raw C code into 20 lines of easily digestable pseudo-C.
We could have gone even further and split the two things that are independent from each other
(main loop, safe termination) into two sections.
You should certainly consider to do so in similar situations.

The key points you should take away are:

- Focus on the important stuff.
- It is okay to modify the code for simplification.
- Shorten until only important things remain.
- Actually *write* about the important things and why they are important.

