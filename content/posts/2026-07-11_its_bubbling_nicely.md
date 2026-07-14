+++
title = "AI bubble as we know it"
weight = 0
updated = 2026-07-14

[extra]
mermaid = true

[taxonomies]
tags = ["llm", "ai", "technology", "opinion", "bubble"]
+++

## Its a bubble

Surely you can see it? If not we seriously need to discuss about few principals behind how technology adaption grows and how money relates to that equation.

It is clear that Artificial Intelligence (which it is not) is here to stay since Large Language Models just are way too powerful tools not to use, but reality also is that how things currently are built they just cant stand. Its like someone built a house and skipped the foundations and used untreated wood for the flooring; basement is wet, flooding and rotting away. No ancient indian burial grounds needed to haunt this mansion.

## Jevons Paradox

What the Jevons paradox is? Its more of a principle, or a "law" conjectured from observations than a paradox, but nevertheless its called that.

Named after 19th century economist William Stanley Jevons the "paradox" describes how when manufacture process or use of an resource becomes more in demand the process also becomes more efficient requiring less of the resource or easier application of the process which leads to better efficiency, larger adaptotion and finally to larger consumption of the resource or application of a process or instaed of reducing it. In other words, when some thing becomes easier or cheaper to manufacture or acquire it tends to bring more consumption or usage with it.

Hank Green of Youtube fame recently made a fantastic video about this which I will summarize here. Please go and see that video (embedded below).

{{ youtube(id="a6sYYrLTOjQ") }}

### The "fungability" ladder aka where Jevons paradox applies

Hank introduces a scale - a framework if you will - to explain how Jevons paradox tends to affect certain commodities differently:

* The spesific products like hot water, plastics and other manufactured goods that have a finite applications once manufactured. Like when hot water got cheap we suddenly started to use it everywhere as it was convinient and thus the requirement of hot water increased so we "manufactured" it more. Either via water heaters in the house or through applying central hot water sources like usually is the case here in Finland when talking about cities and such.
* Materials like "code", transportation and printed text that can be used to move ideas or materials across distances. The distance can be kilometers between factories, but it can also apply to distances between email inboxes, books or chat room servers; where ever ideas propagate basicly.
* Substrates like energy (electricity) have a high "jevonsy" factor as they are malleable to any shape and form and can therefore be made to anything. Our modern world, everything in it, runs with electrity, but we do not manufacture different kind of energy for your phone, car, internet servers, satellites or your toothbrush. Energy is energy and it can flow from place A to B to do whatever and it does not discriminate.

A rough illustration of this concept could be depicted like so:

{% mermaid() %}
graph TD
    %% Node Definitions (Using double circles for a clean circular look)
    A((1. Efficiency<br>Breakthrough)):::blue
    B((2. Reduced<br>Per-Unit Cost)):::blue
    C((3. Behavioral<br>Rebound)):::blue
    D((4. Increased Total<br>Consumption)):::red

    %% Cyclical Path Connections
    A -->|Lowers cost of use| B
    B -->|Encourages more usage| C
    C -->|Drives up demand| D
    D -->|Incentivizes further| A

    %% Styling classes for the circular nodes
    classDef blue fill:#e1f5fe,stroke:#0277bd,stroke-width:3px,color:#01579b,font-weight:bold;
    classDef red fill:#ffebee,stroke:#c62828,stroke-width:3px,color:#b71c1c,font-weight:bold;
    
    %% Apply Styling
    class A,B,C blue;
    class D red;
{% end %}

### Applying Jevons paradox to current AI boom

To re-iterate: there is no "artificial intelligence" just really really large statistical models that guess a lot with extremily high efficiency and success rate!

Hank applies Jevons paradox to Large Language Models (the technology behind our current AI boom) like so:

Code is HIGHLY "jevonsy". Its a material resource, but also a substrate. It is a material that in the past has been limited by the amount of minds dedicated to creating code (the programmers), but its also a substrate that can be used to make almost anything. Like the electricity currently powering the device you use to allow you to read this opinion piece also code creates the user interface and implements required protocols for you to fetch the text over the internet. The same languages and code therefore can be used in any device or used to do different things based on how you sequence it; how you mold the substrate. And because how moldable or fungible code as a resource and substrate is there its more likely that there are more applications that we have not yet applied code to yet to which we have since it has been expensive to do so until now. Since large language models allow one developer to act as a team via agents or for non programmer to create functional code from natural language prompt we most likely do now apply more code to solve problems than what we previously did. Hank even takes this a bit further arguing that intelligence itself is an substrate that has been limited by human brain capasity so far and automation via LLMs now augment that - drastically. Note, augments, does not replace or substitute; LLMs are way too dump for that and, no, we wont see AGI in the next decade either.

And here we now start to get to the gist of what I argued already [previously](@/posts/2026-04-21_what_the_llm_future_will_look_like.md), but with just different words and perhaps a much more "scientific" approach to things.

As we use AI (Large language models) more our electricity usage has jumped up. This requires all sorts of investments into infrastructure like power plants, grid capasity build up and datacenters to house the cpu and gpu units running the models. We are in the rebound phase of the cycle. And the rebound phase gets its momentum from economics that dont make sense at all when looked under a microscope.

## Economics is an abusive mistress

There is no escaping the Capital Cycle Theory, at least while we live in a capitalist system. One might argue that we are entering to post-capitalist system, but still money talks, walks and breaths. Perhaps painfully, but it still does so we have to take the old advise "follow the money" by heart yet again and see where it takes us.

As I previously ranted in another post couple months back the capital expenditures are astronomical and this house of cards cant stand. $725 billion a year, thats $2 billion a day or $23000 every second is spent on AI investments right now. Nobody knows the exact numbers, but they are ridicilious. One can argue, and get firesupport from very clever Harward economists is that the AI buildout (investements in infrastructure and software that runs LLM models) made only up to 4% of United States gross domestic product (GDP) in the first half of 2025, but it accounted for 92% of all US economic growth. Without it US ecomony might be in the decline or the very least flat lining around 1%.

The ridiciliousness arises from the fact that we have seen this already; as a species multiple times and as a xennial/elder minnelial I've personalle witnessed this at least twice already. The cycle repeats predictably.

Like the Jevons Paradox (or a law imo) implies as we are now in the rebound phase after initial substrate (intelligence) efficiency factor jump we still just need to dump more and more money in to get to the next efficiency jump, but that might not be actually what is happening. Instead we are seeing a bubble due to another theory. What we are cought in and which will ultimately prevent us from reaching the next efficiency jump is due to Capital Cycle Theory.

{{ youtube(id="2J2Fb1bBufA") }}

Its a bubble. Current AI demand figures are being artificially constructed. Money moves in a continuous loop among AI players to create the illusion of end-demand: Nvidia funds OpenAI -> OpenAI pays Oracle -> Oracle buys Nvidia chips; rince & repeat. Every time money changes hands in this circle, it is double-counted as brand-new revenue. This directly what happened back in the late-1990s fibre bubble in the US, where equipment manufacturers lent money to their own customers just to book it as growth narrative. To certain extent the same happened simultaneously over many industries as the dot com bubble was inflating and the fibre bubble was just a very tangible example of that. "Casual Finance" on their video above also point many other examples from previous CENTURIES. So this thing is not new.

Coined by legendary investor Sir John Templeton, the "four most dangerous words in investing" are: "This time it's different." Believing the current economic cycle is uniquely exempt from historical laws often leads to ignoring risk and repeating past financial bubbles.

So what evidence of a bubble we have?
* Over-allocation of capital
* Artificial circular demand (vendor financing)
* Severe GDP distortion, in the US, but since EU uses mostly US tech still its a number that must be kept in mind.
* Running LLM business never was profitable, but the situation is collapsing rapidly even more. We are already seeing price hikes and token limits being applied across all forms of usage for the LLMs except local models.
* Unsustainable user retention costs / exploding marketing costs
* All tech stocks right now are "priced to perfection" and markets are hyper sensitive. Even a small re-alignment like the one from Broadcom can trigger a meltdown. Guidance from Broadcom around trivial "few hundred million" triggered a violent event that wiped $300 billion from its value in single session.

Its a powder geg waiting to explode, implode and burst. All these things simultaneously.

## Final words

AI and LLMs are not going to go away. They are really good tools when applied correctly, but the way we are currently using them volunterarily and invalunterarily is not sustainable. Its a mirage of efficiency and because of economic realities the mirage will fade away and what is left are the choppy seas and few whale carcasses on the beach. Lets see what tech giants will end up rotting away on the sand once all of this is over.
