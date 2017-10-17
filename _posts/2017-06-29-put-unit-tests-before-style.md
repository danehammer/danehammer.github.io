---

title:  "Put Unit Tests Before Style"
categories: devops
---

> "Aw, man! My pull request failed the style check! Here I'll just fix that real quick and push..."

One of the common strategies used when adopting DevOps principles is creating a pipeline. A pipeline for building your code, a pipeline for vetting your configuration files, a pipeline that pulls those two aforementioned pipelines together and deploys something. It makes a lot of sense. Once you shake up the ITIL-inspired ceremonies with some effort to push work, instead of having Ops pull in whatever's done at the end of the quarter, the sophistication of tools for pipelines is a great fit.

## I <3 Pipelines

Pipelines are a simple way to think about the push model. They become a series of gates for new work product to pass through. Work that passes all the gates, goes into production. Like a series of security checks at the airport.

Example gates folks often use:
  * "We'll deploy it to the QA environment if all the unit tests pass."
  * "Prevent releasing anything that matched against our CVE scanning tool."
  * "Run some set of static analysis on pull requests to lessen the cognitive load during peer reviews"

But last one is what I wanted to talk about. It's those pipeline checks we sometimes add to test for _style_, or _lint_. If you're not familiar, let me explain. When a code base gets large enough, or a team gets large enough, or someone joins the team that keeps using 3 spaces for tab length (!!!), it can be reasonable to use source controlled IDE settings, or a linter run with the build, or a pipeline gate, to ensure code doesn't get merged to the main code line that violates the team's (or the community's, or [Mr. Batsov's][3], ...) standards for code style. Sometimes this is done so you can't use the easy button to merge something that violates the style checker.

Now, I have totally griped, grumbled, and gnashed my teeth over someone pull requesting 80 lines of code changes, that came bundled with 800 lines of whitespace changes. I've also gotten lazy and tacked on a commit just like that to a pull request. It's difficult to filter through. I get it. You see a bot doing patch static analysis on one of the more sophisticated Apache project's JIRAs and you say "I gotta have that." _Caveat emptor._

## What Not to Do

What I want you to watch out for, is that you're not getting carried away tacking on gates in the wrong order of priority. Sometimes when we get something shiny, like seeing all the cool things you can do with SaaS offerings in concert (a common one is GitHub pull requests + Travis CI), we just throw the easiest ones on there and put a _TODO_ to get to those hard ones sooner. See anyone's clone of [hubot][1], there will be all the fun out of the box scripts that can drop one-to-many random images of pugs in your slack, but actually getting auth figured out for prod deployments is still W.I.P.

The author of [How to Steal Like an Artist][2] stated the only advice people give is really just them speaking to their younger selves. And my advice to younger Dane is this:

Make sure your pipeline is adding meaningful quality measures. Keep the noise low, and the signal high.

One signal that every pipeline needs is "did the automated tests pass?". This is immensely useful to do on every pull request. It's a gate that says "don't merge anything that increases the number of failing tests." Regardless of where you are on your journey to adopt some version of automated testing, you can use that.

Well, unless you have zero tests. Go ahead and fail the build for that. But don't worry about style before testing.

Once you have tests for the code being changed, then we can care if it's styled correctly. We can care if it meets [Mr. Batsov's][3] standards. In fact, it'd be pretty darn cool if you could have your pipeline only lint lines that are covered by the test suite. Someone make me that Jenkins plugin, please.

Oh, and just full transparency, I only bring this up because I caught a bug that was introduced by following the direction of the linter. We changed a pattern to something equivalent, but there was a bug in the lint rule. Because there were no tests, we didn't realize passing the style check broke the code.

[1]: https://hubot.github.com/
[2]: https://www.amazon.com/dp/B0074QGGK6/ref=dp-kindle-redirect?_encoding=UTF8&btkr=1
[3]: https://github.com/bbatsov/rubocop
