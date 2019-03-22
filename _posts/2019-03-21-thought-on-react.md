---

title:  "Thoughts on React"
categories: programming
---

My feelings about React are mixed. On one hand, it's an elegant framework, I
like working in it. I just love how it feels. But I can only get there if I
check a few things at the door. Part of my mind wants to throw React out from
the start because SPAs tend to be bloated, and  JavaScript is an evil
king that I pray to be overthrown. But React is really freakin' fun! Alas, the
woes of software development.

### Experiences

When I joined Udacity in Fall 2017, I had effectively zero front-end
experience. I had hacked up a UI in [Google Web Toolkit (GWT)](http://www.gwtproject.org/)
years and years ago. I had tweaked HTML before. But this really made me more
dangerous than helpful.

Early on in my time at Udacity, I would find myself working on fixes or
improvements to our back-end auth services, and wanting to "finish" the work
by augmenting the front-end code to use the changes. This led me to tinkering
with the React app dedicated to sign up and sign in. That led me to reading
source code of other React apps. Then I finally took advantage of the free
nanodegree perk for Udacity employees, and started studying React in earnest.

Having now completed the React nanodegree, I'm having an easier time getting
through the aforementioned, bag-checking doorway. There are some good reasons
to bring in more dependencies (like redux). That does make the bundle size
larger, but you can make some pretty sweet SPAs in this world. Like
everything in software, it's a trade-off. And sometimes a 1 MB .js file is
worth it. Although, it's almost certainly not worth it near as often as it's
done!

### Pros

#### Composition

Emphasizing composition of smaller pieces makes refactoring easier. Which is
good, marketing constantly wants to tweak the pages users see. 😄

#### Declarative Code

Following React conventions, you get quasi-HTML snippets that read very
differently than some alternatives, say an .erb. Your component has to
separate the rendering, and the state changes. It cleanly gets your mind
following state changes. If you have done much functional programming, it can
be easy to just say "never have state!". That's a beginner's mindset, anyway,
and a useful one. But you _need_ state as the user fills out a form, gets an
error displayed to them, etc. The way React puts state changes in your face,
and gives you clean ways of handling them, is delightful.  

### Next Up

Code splitting and server-side rendering (SSR). I want to use React as much as
I can for front-ends, while limiting how much data needs to be transferred to
load the page. Experimenting with these two approaches should give me some
better understanding of how hard that is to pull off.   
