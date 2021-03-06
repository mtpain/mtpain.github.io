---
title: Theory and Tools of Lean Software Development 
tags: software development
layout: post
date: 2015-01-29
---

Introduction 
============

Lean software development focuses on increasing the speed of delivery
and quality of products by reducing waste. Agile software development
philosophy complements lean ideas, maybe most vividly through one of the
lines of the [Manifesto for Agile Software
Development](http://agilemanifesto.org/) is that agile software
development should “respond to change over following a plan.” The
biggest devil we face as developers is partially done work, the root of
all waste. We can often avoid partially done work by holding each other
to documentation and unittesting standards and by putting off commitment
to a particular *way* of doing something until the very last minute.
Communication is king, and customer collaboration is a must so that we
don’t build something that nobody wants. Instead of delivering a product
that fills every possible customer desire, we will focus on “minimum
useful feature sets” which we deploy *one at a time*. What follows is a
summary essay of industy best practices for managing large software
projects.

Theory: Lines of Code are Inventory
===================================

Lean software development is an adaptation of lean manufacturing
principles to software development. The term “lean” comes from the
obsession with cutting all wastes. In order to “help reinforce the habit
of seeing waste” [Poppendieck,
2007](http://books.google.com/books/about/Implementing_Lean_Software_Development.html?id=3TM0AgAAQBAJ)
here are seven wastes, and from the reduction of these seven wastes, all
other principles of lean software development flow.

The seven wastes of software engineering
----------------------------------------

1.  Partially done work

2.  Extra Features

3.  Relearning

4.  Handoffs

5.  Task Switching

6.  Delays

7.  Defects

By focusing on eliminating these wastes, we are actually focusing on
producing quality code.

Some examples of how reducing waste translates to quality software
------------------------------------------------------------------

Oftentimes in software projects, there is some deadline that is crushing
everyone’s soul, and the most expedient thing to do seems to be to get
the software to “just work” as quickly as possible. Unfortunately, that
usually guarantees more work and less free time in the future for the
next developer who works on the project. By rushing through a project
and not considering how to build quality in, we inevitably build up a
“technical debt” that will need to be payed off at some point.

There are many ways to build up technical debt, and technical debt can
be thought of as the result of failing to handle waste properly. For
example, if one developer creates a new feature, but doesn’t write
tests, the app gets deployed, and the feature breaks, we have lost a
means for identifying the reason for the breakage. If the developer had
written unit tests, the team would know that everything tested was not
to blame; the tests reduce the degrees of freedom of what could go
wrong.

Unittests are also a form of documentation, but can’t be the only form.
We further accumulate technical debt when we don’t write code
documentation. Documentation includes code comments, which should say
why the code is doing what it’s doing and why it’s written a certain
way. The code itself should be expressive enough to say what it’s doing.

Handoffs are inevitable and desirable: no developer will work on a
project his entire career, or often not even for more than a year. But,
if unittests or documentation is missing, this will increase the
*Relearning* that has to happen in order for other developers to pick up
a past developer’s work. Ultimately what this means is that, if a
developer has not written unittests or documentation, then they have not
actually finished their work. So a defect is a waste, but it is
exacerbated by what may be the ultimate waste *partially done work*.

All other wastes stem from partially done work. Extra features are
partially done work. If a feature is not needed, but it hangs around in
a codebase, then it presents the possibility of breakage. It is
inventory that is sitting in a dusty warehouse with a roof leak. It’s
only cost, no benefit. If the responsible developer had just deleted
such excess while it was relevant, no future developer would have to
*relearn* which features were important and which weren’t.

The absence of waste is speed
=============================

What does a project look like when there is no waste? We’ll address that
by an example from the book [Scrum: The Art of Doing Twice the Work in
Half the
Time](http://books.google.com/books/about/Scrum.html?id=93tIAwAAQBAJ).
It is the story of a new FBI data management system called Sentinel,
which after four of five years gone in a contract to the mega-contractor
Lockheed Martin, was overbudget and had zero demonstrable progress
except for ever-more elaborate Gantt charts which had to be constantly
updated because numerous deadlines just kept passing by like cottonwood
on a summer day.

Finally, new leadership abandoned the old plan and started anew, and
promised that by or shortly after the end of the contract delivery date,
a working, pleasing system would be in place. To stay under budget, many
workers were let go of their project responsibilities. By having weekly
scrum meetings and implementing other lean and agile ideas, they stunned
all stakeholders by delivering as promised in a much shorter timeframe
with a much smaller team that had been originally planned. The bigwigs
who were raised on Gantt charts just couldn’t understand how the team
succeeded.

The truth is that for large projects, such Gantt chart management is
proven to be inferior to Agile methods. The basis of Agile methods is
the Scrum, which is further fortified by the concept of Kanban, a word
built from two Japanese words: *kan*, which means *card*, and *ban*,
which means *board*. The *kanban* is just that: a board with cards on
it. On the board there are columns drawn which represent different
stages of work, e.g. planning, implementation, testing, and production.
There are also rows drawn, with each row representing a task within a
larger project, like, “add a sliding sidebar with options to the home
page”.

The reason Gantt charts are inferior and Agile methods superior is each
method’s ability to handle change and complexity. In the Gantt chart
approach, all complexity is to be handled from the outset since
everything must be planned for in detail. However, as Dwight D.
Eisenhower said, “In war plans are useless, but planning is
indispensible”. There is planning that must be done, and at some level a
Gantt-type chart may be useful for this. But it can only go so far.
Agile methods depend on continuous feedback from developers and
customers. Nothing should be committed to before it’s necessary to
commit to it. For example, if a new web page is being designed, it’s not
really necessary to choose a web server or a framework before the
general design and goals have been agreed upon. Indeed, committing to a
particular solution before it’s necessary is a *waste*, since new
information could come to light that would render such a decision null
and void, and then developers must go back to the drawing board anyway.
Why not leave that decision for later when we have more knowledge of the
requirements and complexity.

Tools for reducing waste and improving speed
============================================

In order to reduce waste, we said that all team members must be invested
in the project and in a state of contiual learning and development. One
of our key goals is to generate knowledge. But how do we collaborate
effectively? There are plenty of tools to help us do that. Perhaps the
most important tool is also one we can feasibly start using immediately:
the git version control system and a git server with a user interface
and productivity add-ons like Github.

Git and Github
--------------

Git is a version control system. At its root, this means that git tracks
different versions of a given code base and provide tools to compare and
merge those different versions. These different versions are called
branches. In Git there is a master branch which would correspond to the
stable, public version of the codebase. When we use git for our NKN
Portal, the master branch will be the code that is public facing. If,
say, we wanted to add support for some advanced searching features, we
might create a new branch called `search`, which at the time of its
creation is identical to the master branch.

Git tracks incremental progress every time a user *commits* their
changes locally. When a developer is finished with a feature or issue,
the developer *pushes* changes to the server, for all contributors to
see, a list of commits that the pusher made is shown. Every commit gets
a unique identifier, so that if, for example, some new feature broke the
website in some way, it is easy to revert to a known working version.

Tracking contributions is one important aspect of git. Github builds on
this tracking by providing us with concepts like “Milestones” which are
met when all of the *issues* associated with that milestone. So, when we
are developing the next iteration of the website, we may have a
milestone called “Wireframe” where we just get the first draft of the
structure of the data portal. The next milestone might be called `beta`
testing where we invite select partners and collaborators to test the
site and give us feedback.

Tracking these issues in git is handy enough in itself, but it gains new
power when we transform those issues into a card for our Kanban board.

Kanban board online or in person
--------------------------------

Kanban boards are a simple tool with truly magical results. The Kanban
board focuses our sprints and scrums. We can track each other’s
progress. There is one online tool I’d like to use, called
[Taiga](https://taiga.io/) (https://taiga.io). Taiga is really simple.
You create a project and then create cards. Although a sprint may be
slated for two weeks, the lean approach warns us about taking such a
time frame too seriously. If it takes longer for the product to be done
right, that is OK. The kanban board helps us better allocate
person-hours and predict how long a sprint actually *will* take.

As we said before, a kanban board has columns, which correspond to
stages in a project, rows which correspond to a user story’s path. A
card contains a very specific “user story” or issue, or task, that needs
to be taken from planning to designing to development to final testing
and finally to be deployed. The project manager is largely responsible
for creating the cards, and to a lesser extent responsible for
delegating tasks. Developers are encouraged to identify which tasks they
have time and talents to tackle.

Automatic Documentation Tools
-----------------------------

“Create knowledge” is one of the seven principles of lean software
development. We don’t consider code finished until the documentation
exists: undocumented code is partially finished work. Conversely,
uncoded but documented code is also partially done work, and it’s a
commitment to something that doesn’t yet exist: the documentation gets
generated *along with* the code. No documentation should be done before
the code is generated, and really only final touches should be done at
the very end of a sprint.

In order to facilitate documentation generation, we need to take
advantage of automatic documentation tools like Python’s [Sphinx]()
package, where an entire module of classes and functions can be
documented with a single line of code, using in-file code comments to
build the content around function signatures. Such tools can be
integrated with other tools that the team agrees are acceptable, like
AsciiDoc or LaTeX.

Unittests and continuous integration
------------------------------------

Unittests are how we build quality in. Test-driven development is a big
topic in itself, but it is also a key element of lean software
development. By this, we focus what code we’ll actually write by first
writing what *should* happen, what is the expected behavior of our code.
In this way, we stay focused on writing the code that solves a specific
problem. It helps us understand what the independent parts of our code
actually are. Functions are kept more concise since each function gets
tested independently.

Continuous integration servers run unittests on every branch that gets
pushed to the “remote”, reference git server. Thus every person on the
team knows the status of each branch, and everyone has confidence that
updates to the master branch won’t break other parts of the code.

Focus on User Stories
==================

We need to better understand our customers. We need customer stories. We
need to ask what we can do to improve their experience. Let’s center our
sprints and milestones on the needs and wants of our customers. Let’s
delight our customers. Let’s surprise them with something they never
knew they wanted and now can’t live without.

