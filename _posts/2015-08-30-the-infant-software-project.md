---

title:  "The Infant Software Project"
categories: devops
---

I have noticed a disconnect around expectations of software projects that are "done."
When a dev team is ready to take a software project to prod, it might be in various
stages of its lifecycle. It may be an infant, with no ability to feed itself, and
all it can really do is get people to say "oooh."

On the other hand, there is often an expectation from the Ops team, that if you're
ready to take it to prod, it's an adult. Maybe a young adult, but still an adult.
It takes care of itself, it knows all the things that go in to being a software
project in prod (monitoring, logging, not killing yourself with garbage \[collection]).

I think this is made worse by the notion of a "Minimum Viable Product". Not to
say we shouldn't continue on our use of Agile principles, taking MVPs to prod and
getting feedback much faster. But go talk to each other, early and often, where
the feedback from talking has time to be used in the ongoing development.

Like most disconnects, the problem is in communication. If I go by my default
behavior as a dev, I will likely keep things simple by not worrying about long
running processes, or logging and monitoring, or how it will be deployed. If a
sysadmin starts with the minimum viable, that might be all a process did!

Development teams have to understand that MVP does not mean it's not good, it's
not polished, but that it doesn't do everything it might need to do.

Operations teams have to understand where they can really shine in making the
MVP successful, helping ask the right questions about operations concerns in
the midst of that early development. That way when we take the infant to prod,
its got all the things a baby would have, a properly sized car seat, feeding
arrangements, and the like.

Then when that perfectly timed feedback arrives, we make it into the child and
adolescent the customer wants! Not what dev wants, not what ops wants, but what
the customer wants.
