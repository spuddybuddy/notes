April 9, 2019
spuddybuddy@ubertuber.org

In casual conversation at work I use the following terms to describe the kinds
of problems I have deal with in software.

# Interesting

These problems are simple to describe, and conceptually simple to solve, but
there are multiple potential solutions with advantages and drawbacks.  No single
solution is the obvious choice and it requires some digging into assumptions,
requirements and sometimes prototyping to figure out which solution to pursue.

Many regular software engineering problems fall in this category and can usually
be resolved in days or weeks.  I've worked on bunch of interesting problems over
the years.

# Hard

These problems are simple to describe, and conceptually simple to solve, but
implementing that solution involves deep changes to complex systems and carries
many risks and unknowns.  There are lots of corner cases and it's impossible to
anctipate all of the impacts up front.  In general, these problems are
impossible to solve the right way 100% of the time.

Solving these kinds of problems require up-front research and careful planning
of the implementation and rollout.  Investment in testing and a process for
iterating on the solution without regressions are imperative to maintaining
quality bar for the user experience you're trying to enable.

It usually takes months, sometimes a year or more to fully land a hard problem.

Examples of "hard" problems my team has worked on include Cast Streaming and
Media Remoting.

# Research Problem

A research problem is open ended.  You might be able to recognize what a good
solution is, but there's no obvious way to get there, and the effectiveness of a
given solution might be driven by subjective measures.  The range of things you
might try is heavily guided by assumptions and reasonable people will disagree
on whether one approach is even worth trying or not.

These problems need a lot of up front work in defining the problem and what a
good solution looks like, even before solutions are proposed.  Agreeing on
concrete behaviors that describe a good solution and figuring out how to measure
them is a big part of the initial work.  The effort can then shift to continuous
prototyping and experimentation.

Particularly promising approaches can be forked off and then it can be
determined whether they are feasible for integration into existing systems.
Often others are given the "hard" problem of incorporating the research project
into an existing product or code base.

These projects take years, and may never be fully complete.

Examples of a research problems I've worked on (outside of graduate school) are
new Web APIs like the Presentation API or Internet protocols like the Open
Screen Protocol.






