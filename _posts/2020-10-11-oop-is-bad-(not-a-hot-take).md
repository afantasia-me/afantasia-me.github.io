---
layout: post
title: OOP is Bad (not a hot-take)
date: 2020-10-11
updated: 2022-09-07
tags:
  - Computers
  - Programming Languages
---

[https://www.youtube.com/watch?v=QM1iUe6IofM](https://www.youtube.com/watch?v=QM1iUe6IofM)

Related reading but not directly addressed, just part of the reason why the below is not a hot-take: 

[Why OO Sucks](http://www.cs.otago.ac.nz/staffpriv/ok/Joe-Hates-OO.htm)

[Bad Engineering Properties of Object-Oriented Language](http://lucacardelli.name/Papers/BadPropertiesOfOO.html)

[The faster you unlearn OOP, the better for you and your software](https://dpc.pw/the-faster-you-unlearn-oop-the-better-for-you-and-your-software)

[Object Oriented Programming is an expensive disaster which must end](http://www.smashcompany.com/technology/object-oriented-programming-is-an-expensive-disaster-which-must-end)

I do agree with the fundamental thesis that OOP is flawed and worse than either a structured procedural language in the majority of programming uses, though I am predicating that I also know of some cases and ways in which the fundamental idea behind the original "OOP" (as coined by Alan Kay, and as seen by Smalltalk, Self, and then solved without the mess in Erlang as this "messaging oriented programming" instead) truly shines through as a superb way of tackling certain problems (primarily where fault tolerance a la Erlang is the key, and where passing messages between many conceptually simple components gives the system you can reason most about), but that this is not the majority of cases, and that many of the ways it can be used (graphical systems) it is either an equal to other methods or considerably worse (callback hell, god objects, dependency graph hell, etc), and that Java does typify some of the worst of all this, and the only reason C++ gets nowhere near as much ire is that you can drop back down closer to the level of C (but unfortunately it's difficult once some "OOP" parts are used as it's almost infectious, eg. destructors etc). Generally, I agree that "managing" state is essential, and where possible eliminating either the need to manage, or the amount that you are managing, is usually the most reasonable approach, but at the same time there are many situations in which you simply cannot, and so discussing and figuring out how management can be done well is an important part of the challenge of "good" language design.

Now, tracking the history, it was indeed with the actual introduction of structured programming that the first ideas beyond simply the syntactic structuring of code began to take shape, and in those original papers from Dijkstra and co we begin to see them develop a semantic structuring of code and, by extension, data, giving some of the notions of referential objects, and that to push people from having all this data just loosely and freely accessible, they gave a notion of accessing data over these referential graphs and hierarchies — but this was about structuring data and its flow, which is where most OOP failed and devolved into equally meaningless graphs where everything is fully connected (if not directly then transitively, thus the whole "you get a banana and the entire forest"). We did see this structuring take place more effectively in C (ironically) because data tended to flow up and down hierarchically due to the fact that we weren't creating objects that floated around and handled their own processing, and also because we tend to create these limited silos of global data by design, with the majority of additional data being passed hierarchically "by context" through a single uninterrupted thread of control and dataflow. Yes, it's not just single-threaded, but that notion of single threads of dataflow tends to generalise to the parallel cases as usually we have "embarrassingly parallel" code where we have lots of little threads with basically no interaction and thus it's just "a single thread of data flow, just processing more than one at once", or we have fewer and more interlocking cases of parallelism, where we tend to then have a single thread of "parallel control", which synchronises things and keeps it sane — however, as this scales, the case for message passing like with Erlang becomes stronger, particularly where you can have self-organisation without strict global oversight by a single thread; one of the strongest cases for designs like Erlang is the massively distributed compute problems it has been used so successfully in.

This similarly occurs in functional programming, and in the Lisp-likes it is for the same reason as the procedural languages thanks to scoping, while in the pure functional languages it ends up being for the fact that data is generally immutable, and so you don't keep lasting references to something and modifying it in the same way you might in Java (among other differences that help with pure functional). Now, that's not to say these won't get complicated, however in these cases I would say that the early "object" languages like Smalltalk and Self actually resembled Lisp far more than, say, Java resembles Smalltalk. Similarly, Erlang resembles Smalltalk and Self extremely closely, it just took a more imperative approach and avoided the "OOP hype" traps that Java and others fell into. Notably, concepts such as subtyping and embedding and "prototyping" are far superior to what is displayed by most OOP languages, and the original work in these areas far outstripped what Sun and Stroustrup implemented later with "classes" and their flawed notions of inheritance, so I won't cover them here as type theory is far richer without the discussion of these failures.

Now, the call graphs and dependencies for data are still complicated, though far shallower and ironically end up more structured than most Java code. From what I recall the "solution" that he comes to in a later video is to use a relational model of programming, which really doesn't mean much at face value considering the majority of relational modelling is through the lens of SQL, which is not what we want because SQL is *utter garbage*. However, taking the model of a relational algebra (or tuple/domain relational calculus, they're all equivalent, and we can see where this might be useful in a bit) and applying it properly to a programming language (beyond QUEL etc), and we can start to see there are many areas where this starts to be a nice idea (certainly on the surface, though there's a lot of detail to get into here so I'll only briefly skim over it). Nominally, the idea that the relations between entities is the critical aspect for us to model, and why OOP people became so obsessed with drawing out object graphs, is because a lot of the complexity in a system is based on what connects to what, and understanding it as these entities/components that *relate* to one another gives a very strong tool for diving into the complexity of many systems.

If a hypothetical language in this format (I'll call it Rem for "Relational Model" and Trigun) were to allow us to express these entities (which are just "plain old data" for the most part, so I'll call them types), constraints of these types, ways in which these types relate to one another, and then allow us to start organising ways in which constraints and triggers can start to set of events, chains of events, and start querying and transforming the data and then storing/outputting/using it... and that this was actually a sane undertaking (Rem would not look like SQL, and honestly a purely textual interface is just too limiting for something like this, so while it could be like that I also think it would truly benefit from greater "IDE" tooling in a sense far beyond just what we currently have, and that graphical elements and ways to visualise and formalise what's going on would be a hugely important part of it) then this is starting to be something that can start to solve *some* problems.

I say *some* because ultimately, whilst something like SQL *can* be used for actual computation, there are hugely limiting parts that prevent it from being a *good tool* for most needs, and where the way we present and handle the "relational" part of the model becomes a burden that makes things overly complicated. This is where the part I mentioned before that "relational algebra" and "relational calculus" are equivalent — this is a mathematical fact, and something already levied in query optimisation, and where we might start to move beyond some of the disconnect between the "imperative" and "declarative" languages (notice that I hadn't mentioned this yet, there was a reason and not just "declarative doesn't actually mean anything"). The idea here is that we can start to write something in a very high level fashion, where the constructs and primitives we use are describing the goal state and the constraints involved in it, for example: the goal may be moving money around, but the constraint is double-entry bookkeeping (that every transaction has an equal and opposite "reaction", ie. money is never created out of thin air) and has very fixed rules for introduction and destruction. This is starting to resemble "declarative" languages, in particular logic languages (and there's a good reason for that) so let's unpack what that actually means.

Current "declarative" languages fall into two camps: languages with a comprehensive standard library that can handle goal solving (ie. Haskell), and languages where their primitives are literally goal solving (logic languages, eg. Prolog). Now, the first camp is clearly not *really* a declarative language, and in these cases implementing these "goal solving" methods in languages such as C is an important tool that many programmers use (for example, search algorithms, optimisation algorithms, etc) means that we can really declassify them and point out that there really is no point to "declarative programming" as an *identifying* parameter. There is, however, meaning to having it easily expressed as per logic languages (and DSLs), and that is this idea of "language as a tool of thought", where language shapes mind and mind shapes language (not just in computers but also real) where we consider more than just the "grammar" of the language: the meaning, the way it is used, the context. In programming, we see C++ being carved up into these "dialects" where different companies and programmers use different parts of the language, and favour the usage of some parts more than others, and view the usage of particular parts as taboo. This is an extremely revealing thing, because we can see that the impact on mindset and *how* people solve problems is (in part) influenced by the very design of the language itself. Logic languages are trying to solve in terms of these goals and constraints, which is superb for logic, and this becomes an extremely valuable tool in the "programmer's toolbox", however the adage of "once you have a hammer" (or Adam Savage's variant, "every tool's a hammer") does ring true and this is precisely the issue that OOP, functional, "declarative", logical, and even our supposed "relational" programming languages all fall prey to: they master their tool and fail to serve anything else to the same capacity, meaning you eventually hit a wall and have issues.

So, reading between the lines suggests that I like "imperative" programming, and indeed I do. Again, reading between the lines, I also like "procedural" programming, and indeed I do as well. In fact, you could almost say I like "procedural" and "imperative" programming, and since I also like "structured" programming then I would say that something like C is pretty swell (oh boy it has issues, but that's the topic for another time perhaps).

And this is where things get interesting. See, as I mentioned, we can start to move beyond a "disconnect" between the declarative programming we think of with logic languages (and proposed for Rem) and the imperative programming I say I like, and that language usage suggests is still the key thing common to the overwhelming majority of languages still in use — namely they're all structured, imperative, and procedural... or rather, at least those three components form the core of basically all languages that are even fractionally popular. Ah, we can have a "core" of a language that fits a model? Does that suggest we can have an "exterior" of a language that is different? Say, more "declarative"? Ah, that's the first camp of "declarative" languages we were talking about. Huh. Now we're getting somewhere.

So, if we take this idea of a relational language that can transition from a high level model built around solving "relational networks" for given constraints and goals via transformations of these networks (the events/triggers/queries/functions/etc) in an optimal manner using techniques beyond just query optimisation (both pre-compiled and "on-line"/"just-in-time"/"lazily") and having solving/optimisation techniques beyond depth-first search that are readily accessible to the programmer and not just arbitrarily fixed "by design", with then allowing for this "message passing" I was praising Erlang for to allow networks to resolve themselves locally without need for global oversight or synchronisation and as part of fault-tolerance that allows us to trust in the code which extends into a "relational" fault-tolerance perhaps beyond the kinds of strict relations we currently use in relational modelling and goal/constraint solving, with then the ability to recognise the immutable and how over time our networks & constraints vary and so holding onto "references" is meaningless and so the conceptual model tends towards one of immutability with ad-hoc/local consistency before global consistency, with then the ability to write the procedural code needed to handle the sticky cases or when we need a single thread of control/dataflow or to handle synchronisation properly through a set of steps that allows us to handle disputes and achieve consensus, whilst making use of the equivalence in relational modelling and extending it to make use of our imperative code similarly with the declarative code being able to start to fill in from the toolbox provided by other declarative and imperative code, perhaps even extending such that the "extremely imperative" code we might write in a procedural fashion can actually be translated into a lower level of functional code (lambda calculus all the way down) perhaps even transparently so by showing the equivalences under code-rewriting and optimisation, perhaps extending further to showing proofs of correctness if this extends to bisimulations etc...

Perhaps with all this we're starting to get to the kind of "ideal" "relational" language that perhaps all language design aspires to, and something I'd hope to one day feel confident tackling (maybe you'll see me publish an actual Rem someday), however it's clearly a monumental undertaking.

So, until then, we're left with the jack of all trades that is procedural programming. Everything we've discussed are just tools in the toolbox, so that means I can reach for them even in C, they just might be a little more awkward to wield and a little harder to master than their native tongues... but I suppose that's how the English language has always worked, isn't it?