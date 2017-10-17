---

title:  "A Belated DOES Summary"
categories: devops
---

In October I attended the [DevOps Enterprise Summit][does], a.k.a. DOES. Overall,
it was a great conference. I enjoyed it immensely and hope to attend again next
year. I wanted to share the high points, the most resonant comments; basically
the bits that I scratched down in my notebook or live-tweeted.

#### _What works for the Unicorns can work for the Horses_

This. Stuff. Works. Biggest thing on my mind leaving the conference was the
confirmation that companies all over the world know something some of us don't:
this stuff works. DevOps investments, emphasis on Lean management, identifying
process bottlenecks and improving them, regardless of your technology or stack,
can be used to make you far more successful/profitable/competitive. To explain
the quote, the unicorns are the "magical creatures", the Google's, the Etsy's,
the Netflix's,
where we hear about some of these radical process changes that enable teams
to deploy to prod tens of times a day. The horses, are the rest of us. See
[Nicole Forsgren's talk][forsgren] for more details on how the data proves this.


#### _How Infrastructure Teams work other places_

In my current job and late in my previous one, I was focused on engineering the
infrastructure pieces that enabled feature teams developing customer facing code.
I spend a lot of time thinking about Jenkins plugins and self-service designs.

My favorite talk about this was Mike McGarr's [Beyond the Culture Deck: What You
Don’t Already Know About Netflix][mcgarr]. His metaphor of how feature teams
have a common problem when they want to deliver working code to their consumers
is amazing.

Think of that problem as crossing a river. Everyone has to cross the river. And there are two common approaches to how to enable lots of people to cross a river. The first is using a ferry, and the second is building a bridge. With a bridge, the developer can cross the river at a speed of their choosing, at a time of their choosing, they can go fast, they can go slow, they can stop in the middle of the bridge. They can cross once a month, they can cross multiple times a day. On the other hand, if we employ the ferry strategy, you work at the ferryman’s schedule. If he only crosses on Mondays at 1pm, that’s when you’re crossing the river. If you’re late, you have to wait a week.

And here’s the big differentiator: when you cross a river with a ferry, how much ownership do you feel for crossing successfully? How invested in the process, in its efficiency and excellence? In order to realize the speed, the agility, the competitiveness in the marketplace that we all crave, we have to enable individual teams to be autonomous. They need to be able to own, and drive, everything required to go from "we made a thing" to "users can use the thing."

This metaphor is amazing. The other piece I took from him was (paraphrased), "If
a team has to wait on another team, is it because of knowledge/expertise? or just authorization? And either way, what can we do to remove that gap?"

#### _The Blinding Brilliance of Steven Spear_

Steven Spear's talk, [Creating High Velocity Organizations][spear] was hands down my favorite talk. I have little notes from it, because you can't stop listening to him for a second. I don't have much to add, just go watch this. Twice.

Rickover's process keeps coming to mind since hearing Spear. The ideas of raising your hand and asking questions, even if it's just to show your peers that it's what you do when you don't understand. Finding ways to share knowledge amongst units of the org, and design it right into the process. Have a scientific process for learning!


### My Favorite Sessions (in order)

1. [Steven Spear - Creating High Velocity Organizations][spear]
2. [Mike McGarr - Beyond the Culture Deck: What You Don't Already Know About Netflix][mcgarr]
4. [Jeffrey Snover - The Cultural Battle to remove Windows from Windows Server](https://www.youtube.com/watch?v=3Uvq38XOark)
3. [Tom Limoncelli - Radical Ideas Enterprises Can Learn From The Cloud](https://www.youtube.com/watch?v=4pso_4vfyow)
5. [Nicole Forsgren - How Continuous Delivery and Lean Management Make your DevOps Amazeballs][forsgren]

[does]: http://devopsenterprise.io
[mcgarr]: https://www.youtube.com/watch?v=3hULyTAESBE
[spear]: https://www.youtube.com/watch?v=onwhZwroQHs
[forsgren]: https://www.youtube.com/watch?v=opEKZpAOhIk
