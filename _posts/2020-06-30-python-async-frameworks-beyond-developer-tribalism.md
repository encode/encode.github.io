---
layout: articles
title: "Python async frameworks - Beyond&nbsp;developer&nbsp;tribalism"
permalink: "/articles/python-async-frameworks-beyond-developer-tribalism"
---

<br/>
I've been thinking about writing this article for a bit, but have been most prompted by a post grandly titled "[Async Python is not faster](http://calpaterson.com/async-python-is-not-faster.html)". The post was rooted with some good motivations and observations, but also fell somewhat into a polarising mode of discussion that I'd like to see our communities try to move beyond.

Async concurrency necessarily brings with it an element of ecosystem split, and this can mean that it's a bit of a divisive area to try to have conversations within.

However I think we could probably benefit from a bit more recognition of where there is shared ground. And in areas where there's less clarity, to be able to have constructive conversations around the relative merits in differing approaches.

---

# Some things we probably ought to agree on...

### ★ Why you shouldn't care about "performance".

If you're starting a new project, and choosing a python async framework vs a python sync framework, then any "performance" metrics around the frameworks *almost certainly don't actually matter*, and are almost always a nonsense point of debate.

What is *actually* critical to your business is the development experience and strength of the surrounding ecosystem. What is your time to market going to be? How will the maintenance overhead be? How robust and evolvable is your codebase?

### ★ Why you might care about "performance".

Having said that, there *are* a small portion of cases where the performance characteristics are a valid consideration. Particularly if your web framework makes lots of outgoing HTTP requests or other networking and I/O.

It's important for the Python ecosystem that it ought to compare favourably to other dynamic languages in domains where async is beneficial. We don't want to be in a position where "we're using JavaScript because we believe it'll scale up better" is a valid market blocker vs. choosing Python.

### ★ What we're talking about when we talk about "performance".

Like-for-like a single async function call in isolation will be marginally slower than a plain function call. That's not contentious.

What we're actually interested in is how *efficiently* we can interleave multiple concurrent tasks. In I/O bound systems co-operative concurrency (async) performs more efficiently under high concurrency than threaded concurrency (sync). Again, not contentious.

Again - Async Python is not faster. It *is* more efficient. Which will *tend* to mean that on I/O bound systems, the latency will *continue* to remain low even as the level of concurrency increases.

### ★ There are no good benchmarks.

JSON "hello world" benchmarks are junk. Almost all cases of "I've created this benchmark myself" are likely to be junk. The prevalence of new frameworks overly focusing on nebulous benchmarking claims is generally junk. An obsession on benchmarking numbers can also sometimes result in poor overall design choices, such as obfuscated or unnecessarily coupled bits of codebase, because some not-very-meaningful metric is being prioritised over the code design itself. None of this should be contentious.

It's not *always* true, for example, when Sanic was introduced there was a genuine step forward which was worth talking about, so I can understand why there was a focus there. But there's still a ridiculous hype-cycle attached as a result, and we need to be really careful about trying to step beyond that.

It's also reasonable if benchmarking is discussed in a sensible context and placement. For example, to the extent that Uvicorn and Starlette have discussed performance it has only ever been with a view to making a solid case that having a *properly specified* server/framework boundary API isn't a negative performance consideration. Prior to the introduction of ASGI, Python's async web ecosystem had generally bundled together both the low-level HTTP handling and the high level framework, and there was a notion that needed dispelling that introducing a properly specified separation of concerns wasn't a good approach because *"something something performance something"*.

If you *are* going to look at web framework benchmarks for some very rough first-pass ideas about relative efficiency then the TechEmpower benchmarks should almost certainly be your baseline, since they're at least independent, and have a decent range of test cases. If you're going to diverge from them have some good argument for doing so.

The "Async Python is not faster" benchmarking is a reasonable example here, since it had clearly applied a decent degree of thoughtfulness. Even so there were still problems with the methodology, as [Łukasz Langa did a good job of unpicking](https://twitter.com/llanga/status/1271719778324025349).

Having said that, the TechEmpower benchmarks only show throughput, and don't include any *meaningful* latency information. There's actually a good reason for that, since
comparing latencies is really difficult. You can't arrive at a single "95% latency" figure, because the figure you'll arrive at *also depends on what throughput load you're putting the system under* at the time of measuring the latency.

As a result measuring latency is only ever really meaningful if you're looking at *graphs of how the latencies vary over a range of different throughputs*. Amber Brown's [DjangoCon 2019 keynote talk does a fantastic job of showing some examples here](https://www.youtube.com/watch?v=YxP1I-tm_2c).

### ★ ASGI is a really positive step for the async ecosystem.

Having a decently specified server/framework interface is a *really good thing*. Andrew Godwin's design for ASGI fills this gap with a WSGI-like approach. That has a set of trade-offs, but it's a pretty pragmatic and well rounded choice.

This should not really be contentious.

### ★ It's about functionality.

Async isn't just about achieving higher levels of concurrency-per-server, it also makes it a bunch of new functionality more feasible, including...

* Handling long-lived network connections like Websockets.
* Long-lived HTTP connections and server sent events.
* Dealing with background tasks without necessarily needing a full blown task queue subcomponent.
* Parallelizing outgoing HTTP requests or other high latency I/O.

### ★ Not everything is perfect.

The async ecosystem is far more immature than the existing thread synchronous. There are different challenges there, such as ensuring that [backpressure is handled consistently throughout the various async APIs](https://lucumr.pocoo.org/2020/1/1/async-pressure/), or in [applying the lessons of structured concurrency](https://vorpus.org/blog/notes-on-structured-concurrency-or-go-statement-considered-harmful/).

Nor is the "stdlib asyncio isn't perfect" line a good argument either against asyncio specifically, or against async/await in general.

It's okay that there's still work to do in places. We know.  Let's get that work done.

### ★ Async is harder.

Having to *think* about if a function does or doesn't make I/O or could otherwise block *is unarguably more complex than not having to think about it*. It's also more precise - you're having to think about that for a reason, and done properly it's presenting you with more information as a result. Being able to reason more clearly about which parts of your framework stack do or don't perform I/O has a cost but also brings benefits.

There's an analogy to make there in that writing Python using explicitly enforced typing is likely to be a harder than writing Python in an untyped style. It's harder because you're *also being more precise*. That's not necessarily either good or bad, but it is definitively *different*.

This also gets to the point about why the "[What colour is your function](https://journal.stuffwithstuff.com/2015/02/01/what-color-is-your-function/)" argument isn't actually a good case against async code, even if it seems to make clear sense on first pass. We're coloring our functions because we're *enforcing the exposure of some important information all the way throughout the stack*. That's not an inherently bad thing to do.

---

# Some things that are unclear...

If those are areas where I think we ought to be able to reach consensus on, then there's also a few areas where I think that the possible outcomes are less clear...

### ★ You take the high road, and I'll take the low road.

There's a few different tacks we might take onto introducing async into the Python web framework ecosystem...

* Promoting mostly staying with threaded web frameworks. There's actually a perfectly decent case to make that Python *on the whole* should eschew a *wide move towards async*. That the drawbacks of moving large swathes of the ecosystem towards an async model outweigh the advantages. (Pros: Simpler for the end developer. Huge existing ecosystem.)
* Working towards blended approaches. This is being championed within the Django community which is incrementally adding async support, largely off the back of some Herculean work by Andrew Godwin and others. This approach can either be in the form of adding support for async at the server level, while keeping the framework level strictly thread-synchronous. Or it can gradually start to expose optional async capabilities all the way through the stack. (Pros: Brings along the existing ecosystem, while adding async capabilities when they're needed.)
* Working towards async-native frameworks. (Pros: Lower overall complexity of the stack then blended approach. More efficient since there's less overhead in marshalling between two style all the way through the stack. If we're having to write large amounts of new code then it's not a bad inflection point at which to also rethink and finesse other aspects of how we're putting together new frameworks.)

We can't really say which of these will yield the best dividends. Personally I *happen* to be working in the last of those three slices, simply because I can see a bunch of areas where I can contribute meaningfully towards the ecosystem there.

### ★ Positioning asyncio and Trio

There another big question mark over the relative positioning of asyncio and Trio in the ecosystem. Trio is a newer approach to a Python async framework, that's meticulously designed, and based on the principles of structured concurrency, that have been outlined by it's author, Nathaniel Smith.

The difficulty this brings is that Trio is necessarily incompatible with asyncio, and introduces an ecosystem-split within an ecosystem-split.

There's a few different tacks to dealing with this...

* Improve the stdlib asyncio, based on the design learnings of Trio.
* Keep building up the Trio ecosystem, perhaps eventually aiming for it to become a newer de-facto async library for Python.
* Don't sweat it. It's okay to have multiple different frameworks in this space.

As an end-developer of the frameworks, without having an expertise into their internals it can be difficult to make an informed judgment call as to the relative merits here, tho I can see some value in all three of these.

It should also be said, that this section shouldn't be taken to discount the value of *other* async frameworks like Twisted or Curio, which also have their space.

---

# Optimism

Having been working in the Python async space for a while, I feel like we've generally seen an improvement in the maturity of the discourse around what can potentially be a divisive area.

In spaces I've been workin in it's been a pleasure to work *alongside* the Django communities efforts, even if not directly *within* the Django community.

Having FastAPI succeed on top of Starlette has been similarly rewarding. There's such a mutually constructive attitude between the two different projects which makes it a pleasure to see a higher level framework take more of the spotlight, while working on the supporting scaffolding.

In short this is a call for the benefits of adopting **a genuinely collaborative mindset rather than a competitive mindset**.

We may all working on different little corners of the landscape, but we're can still all appreciate that in the bigger view, we're all working together.
