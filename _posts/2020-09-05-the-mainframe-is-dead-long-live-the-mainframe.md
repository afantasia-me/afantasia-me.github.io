---
layout: post
title: The Mainframe is Dead, Long Live the Mainframe
date: 2020-09-05
updated: 2023-08-30
tags:
  - Computers
---

I really like [The Eternal Mainframe](http://www.winestockwebdesign.com/Essays/Eternal_Mainframe.html) essay, and I'd like to just make a small addendum.

It really just boils down to "we will always have centralised compute (call it whatever you will) even as "edge" compute gets faster as that's just the economics of large persistent databases", there's no wheel or cycle here.

Nobody uses dumb terminals any more because why would you due to the limitations of networking and commoditisation of high-performance hardware, so while we all "focused" on supporting and developing for "personal computers", really it's just always been the "fat client" approach when we consider anything related to networking, the internet, and databases. Personal computing is the offloading of the small to medium scale problems onto the user's hardware that do not require active participation in a database.

The moment you are connecting what people output, or the people themselves, you are inevitably just working into and out of a database, and so this centralised compute is the obvious model. This can be abstracted out over a distributed setup and distributed database, as we already do, but we then (eventually) achieve a local or global consistency (because otherwise what's the point?), so it can be modelled as centralised.

The economics dominate and to ensure we all get the experience we expect, physical locality in the compute is necessary as often as possible to reduce overheads, and so we've always had this centralised compute, it never went away, edge compute was just able to pick up the slack because of increasing power and availability (and reliability, esp. given cellular networks and ISP BS).

"Cloud compute" (just the next step towards ubiquitous "public compute") just commercialises it same way rental and public utilities do, you just have to work out whether renting or owning is right for you, which includes factoring for maintenance and setup. People doing this aren't dumb, and anyone who's stuck around long enough or gone through the history will see the names change, but it all stays the same. Data is the thing that matters, so economics dictate this is what we get.

To end, I'm going to put one of my favourite comments below (almost) verbatim, just because it's so good I'd like to save the click (and help back it up for posterity)

[Are We Overestimating the Number of COBOL Transactions Each Day? - Slashdot:](https://developers.slashdot.org/comments.pl?sid=18156250&cid=61014218)

> Back in the 90's I worked for a bank clearing house and was coding some stuff on PC and there was an NCR mainframe which was actually so far out of support that they were literally collecting spare NCR mainframes from dumpsters to have spare parts. There was simply no point in rewriting the banking code since the mainframe from the 1970's was processing banking transactions for … everything for about 1/3 of all bank customers in the state of Florida at the time. We had an entire building dedicated to paper check processing with machines that reached 5 meter high ceilings lining all the walls. We were ingesting (what I assume was) millions of paper checks a week.
> 
> The mainframe guys didn't see their jobs threatened because unlike nearly every PC technology, on the mainframe, everything is an object and everything is a transaction.
> 
> To compare to a modern approach... an IBM mainframe is:
> - CICS - Function as a Service, similar to Amazon Lambda functions... almost identical in fact.
> - DB2 - Distributed Object storage database with NoSQL support as well as (I think) an ACID compliant SQL query engine as well as tables support
> - JCL - Basically the AWS command line tools for uploading and scheduling Lambda events and transactions
> - RPL3 - A batch language for generating form reports … it's basically a precursor to Crystal Reports... which is mostly dead since paper is too
> - TSO/e or ISPF - something like HTML for presenting the user interface to smart terminals... IBM 3270 terminals were sorta like a web browser in the sense that they support things pages and form controls and had things like the approximate equivalent of Get and Post.
> - COBOL - One of very many programming languages which can be called by the CICS engine
> 
> I suppose I could go on, but overall, these systems are basically self-hosted AWS alternatives which have evolved … slowly and hardened since 1969.
> 
> I should point out that COBOL, while not the most exciting language, is insanely simple. As soon as you understand that you generally don't write programs in Cobol, rather you write functions. You schedule the function to run using JCL (job control language) when an event occurs (a form posted data for example) and then you use object storage and NoSQL style methods to query databases and read or store information for example.
> 
> What people generally don't realize about the mainframe is that it completely and totally lacks a single point of failure. You can have a few nodes or a few million nodes. Storage is distributed naturally across any format from high performance SSD through reel-to-reel tape... even S3 if you really want it.
> - IBM mainframes are (and always have been) a cloud.
> - Load balancers on the way into a mainframe distribute transactions across any available node (just like K8S ingress)
> - Unlike ingress, if a transaction doesn't complete, you can schedule a retry that will try another node
> - Functions are stored as source or binary objects in the common object database
> - Within operator provided constraints, all functions are elastic and location independent.
> - When a transaction comes in, the function associated with the transaction (often referenced with something like a URL) is loaded onto a node.
> - The CPU in the node isn't important. The binary format for IBM mainframes is a virtual machine language and has to be just in time compiled on the node where it will run if a binary wasn't already cached from earlier transactions.
> - The system depended on the terminals to provide user interface functionality. Since the 60's, I had been using declarative UIs and a language like JSON for triggering transactions. The difference being that terminals didn't need responsive UI or single page apps. Instead, when a new page layout was needed, a transaction would request it and it would be loaded from the object store.
> 
> Most every programmer in the business world today is learning and using this stuff. Just, they generally use a different cloud provider where they pay for timesharing on someone else's mainframe... which is what a cloud provider is.
> 
> I simply can't possibly understand why, other than vendor lock in... which if it's IBM, it isn't cheap... but until Ginny gutted it, it was highly reliable... why would anyone have an issue with this?
> 
> If you're a bank, financial institution, etc... it's probably still one of the best architectures you can possibly get your hands on. I spent 60 hours last month trying to figure out how to implement distributed storage in a K8S cluster... and how to implement scheduled rolling backups for it... I spent many additional hours trying to figure out how to automate the entire process of removing a K8S node and adding a new one programmatically, Then there's managing the firmware updates for the physical hardware it's running on... I actually have a 50 or so page document listing all the stupid little things I have to do.... to make a simple web server running OpenFaaS and such.
> 
> What's really funny is that if I get this project going, in the end, I'll have a system which is almost a direct mirror of an IBM mainframe... but running on a bunch of Raspberry Pi like devices (except with proper storage connectivity). It'll be able to handle millions of transactions and will be able to scale to hundreds of nodes.
> 
> But if I needed this system at a bank, I'd just call IBM and ask them to deliver... and I honestly don't care whether the functions are written in COBOL or some other language. it doesn't matter, it's data-in, process data, data out. I would give people grief for writing those functions in low level languages... I'd much rather see COBOL than Python, but I would accept Python long before I accept C or any other language which requires you to reinvent the wheel... every time.
