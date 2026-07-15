+++
title = "AI soup is bubbling nicely"
weight = 0
updated = 2026-07-15

[extra]
mermaid = true

[taxonomies]
tags = ["llm", "ai", "technology", "opinion", "bubble"]
+++

## It's a Bubble

Surely you can see it? If not, we seriously need to discuss a few principles behind how technology adoption grows and how money relates to that equation.

It is clear that Artificial Intelligence (which it is not) is here to stay since Large Language Models are just way too powerful as tools not to use, but the reality is that how things are currently built simply can't stand. It's like someone built a house and skipped the foundations, using untreated wood for the flooring; the basement is wet, flooding, and rotting away. No ancient Indian burial grounds needed to haunt this mansion.

## Jevons Paradox

What is the [Jevons Paradox](https://en.wikipedia.org/wiki/Jevons_paradox)? It's more of a principle, or a "law" conjectured from observations, than a paradox — but nevertheless that is what it is called.

Named after 19th century economist [William Stanley Jevons](https://en.wikipedia.org/wiki/William_Stanley_Jevons), the "paradox" describes how, when a manufacturing process or the use of a resource becomes more efficient, the cost per unit falls — which encourages more usage, drives wider adoption, and ultimately leads to *larger* total consumption of that resource rather than reducing it. In other words, when something becomes easier or cheaper to manufacture or acquire, it tends to bring more consumption or usage with it, not less.

Hank Green of YouTube fame recently made a fantastic video about this which has many great ideas that I use and summarize in this post. Please go and watch that video (embedded below).

{{ youtube(id="a6sYYrLTOjQ") }}

### The "fungibility" ladder — where Jevons paradox applies

Hank introduces a scale — a framework, if you will — to explain how Jevons paradox tends to affect certain commodities differently:

* **Specific products** like hot water, plastics, and other manufactured goods have a finite set of applications once manufactured. When hot water became cheap we suddenly started using it everywhere because it was convenient, and thus the requirement for hot water increased, so we "manufactured" it more — either via water heaters in the home or through centralised hot-water systems, as is typical in Finnish cities.
* **Materials** like code, transportation, and printed text can be used to move ideas or materials across distances. The distance can be kilometres between factories, but it can also apply to the distances between email inboxes, books, or chat-room servers — wherever ideas propagate, basically
* **Substrates** like energy (electricity) have a high "jevonsy" factor as they are malleable to any shape and form and can therefore be made into almost anything. Our modern world — everything in it — runs on electricity, but we do not manufacture a different kind of energy for your phone, car, internet servers, satellites, or your toothbrush. Energy is energy and it can flow from place A to B to do whatever it must, and it does not discriminate.

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

To re-iterate: there is no "artificial intelligence" — just really, really large statistical models that guess a lot with extremely high efficiency and success rate!

Code is HIGHLY "jevonsy". It's a material resource, but also a substrate. It is a material that in the past has been limited by the number of minds dedicated to creating code (the programmers), but it is also a substrate that can be used to make almost anything. Like the electricity currently powering the device you use to read this opinion piece, code creates the user interface and implements the required protocols to fetch the text over the internet.

Therefore the same coding "infrastructure" (languages, frameworks, ...) are used in any device or applied to different things based on how you write it — how you mould the substrate. And because code is such a malleable and fungible resource/substrate, there are likely far more applications to which we have not yet applied code to, simply because it has been too expensive to do so. Since Large Language Models allow one developer to act as a team via agents, or allow a non-programmer to create functional code from a natural language prompt, we now apply more code to solve problems than we ever previously did.

Hank takes this argument a step further, suggesting that intelligence itself is a substrate that has  so far been limited by human brain "availability" (everyone is not a programmer as it takes years to learn the trade), and automation via LLMs now augments that — drastically. Personally I would extend this with a note: *augments*, not replaces or substitutes. LLMs are not intelligent and require an intelligence to prompt them first; and no, we are not seeing an AGI in the next decade or decades. Coding is an easy application (for me) to use as an example here, but this argument works for any trade that can actually gain benefits from LLM models when applied correctly.

And here we start to get to the gist of what I argued [previously](@/posts/2026-04-21_what_the_llm_future_will_look_like.md). This time I'm using more established terminology and scientific theories to make my point instead of just purely ranting on based on my own feelings and biases.

So to summarize, as we use AI (Large Language Models) more, our electricity and infrastructure usage has jumped up. This requires all sorts of investment into infrastructure like power plants, grid capacity build-out, and data centres to house the CPU and GPU units running the models. We are in the rebound phase of the cycle. And the rebound phase gets its momentum from economic mechanisms that have been bent to a breaking point.

## Why These Two Are a Perfect Storm

[Jevons Paradox](https://en.wikipedia.org/wiki/Jevons_paradox) tells us *what happens to consumption* when a resource — especially a substrate — gets cheaper. [Capital Cycle Theory](https://en.wikipedia.org/wiki/Capital_cycle) tells us *what happens to capital* when an industry sees rapid demand growth. Individually, each is interesting. Together, during a substrate-level efficiency jump, they form a self-reinforcing doom loop.

The key insight is this: **Jevons says the technology is real and demand will be permanent. Capital Cycle says the investment wave is not.** The bubble bursting does not disprove Jevons — it is *caused* by Jevons attracting too much capital too fast, before real unit economics can keep up.

{% mermaid() %}
graph TD
    A["LLM reduces cost of<br>'intelligence' substrate"]
    B["Jevons Paradox:<br>demand explodes"]
    C["Capital Cycle Phase 1:<br>Capital floods in, chasing growth"]
    D["Circular vendor financing<br>inflates apparent demand"]
    E["Overcapacity builds;<br>real margins never materialise"]
    F["Capital Cycle Phase 2:<br>Capital exits — BUBBLE BURSTS"]
    G["Real substrate demand survives<br>(Jevons long-run effect)"]
    H["Leaner industry rebuilds<br>on real unit economics"]

    A -->|Jevons kicks in| B
    B -->|Looks like infinite market| C
    C -->|Nvidia→OpenAI→Oracle→Nvidia loop| D
    D -->|Masks overcapacity| E
    E -->|Guidance miss triggers cascade| F
    F -->|Dumb money gone| G
    G -->|Real players remain| H

    style A fill:#e1f5fe,stroke:#0277bd,stroke-width:2px
    style B fill:#e1f5fe,stroke:#0277bd,stroke-width:2px
    style C fill:#fff9c4,stroke:#f9a825,stroke-width:2px
    style D fill:#ffccbc,stroke:#bf360c,stroke-width:2px
    style E fill:#ffccbc,stroke:#bf360c,stroke-width:2px
    style F fill:#ffebee,stroke:#c62828,stroke-width:3px
    style G fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px
    style H fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px
{% end %}

When investment disappears or the compute is priced according to what it actually costs and the usage for LLMs will drop due to this leading to the Jevons cycle to break; there will be no new efficiency gains as there are none to make dispite of what the tech giants keep telling us. Unless some magical new technology appears we are still shifting bits around using silicon in a datacenter that requires infrastructure and energy as a substrate.

## Economics is an abusive mistress

There is no escaping the [Capital Cycle Theory](https://en.wikipedia.org/wiki/Capital_cycle), at least while we live in a capitalist system. One might argue that we are entering a post-capitalist system, but money still talks, walks, and breathes. Perhaps painfully, but it still does — so we have to take the old advice "follow the money" by heart yet again and see where it takes us.

As I previously ranted in [another post](@@/posts/2026-04-21_what_the_llm_future_will_look_like.md) a couple of months back, the capital expenditures are astronomical and this house of cards can't stand. Some figures thrown around go as high as $725 billion a year — that's $2 billion a day or $23,000 every second — is spent on AI investments right now. Nobody knows the exact numbers, but there are attempts to [project them](https://www.gartner.com/en/newsroom/press-releases/2026-05-19-gartner-forecasts-worldwide-ai-spending-to-grow-47-percent-in-2026). One can argue, and get backing from Harvard economists, that the AI build-out (investments in infrastructure and software running LLM models) made up only around 4% of United States gross domestic product (GDP) in the first half of 2025, [yet it accounted for 92% of all US economic growth](https://finance.yahoo.com/news/most-us-growth-now-rides-213011552.html). Without it, the US economy might be in decline or at the very least flat-lining.

The ridiculousness arises from the fact that we have seen this before — as a species, multiple times — and as a xennial/elder millennial I've personally witnessed it at least twice during my lifetime. The cycle repeats predictably.

As the Jevons Paradox implies, we are now in the rebound phase after the initial substrate (intelligence) efficiency jump, and we think that we need to pour more and more money in to it reach the next efficiency jump. But that may not be what is actually happening; instead, we are seeing a bubble forming like the Capital Cycle Theory predicts. What we are caught in — and what will ultimately prevent us from reaching the next efficiency jump — is that flood of "dump" capital.

{{ youtube(id="2J2Fb1bBufA") }}

Current AI demand figures are being artificially constructed. Money moves in a continuous loop among AI players to create the illusion of end-demand: Nvidia funds OpenAI → OpenAI pays Oracle → Oracle buys Nvidia chips; rinse & repeat is the defacto example and there are so many players in that graph that its is impossible to illustrate properly.

Every time money changes hands in this circle, it is double-counted as brand-new revenue. This is directly what happened back in the [late-1990s fibre bubble](https://en.wikipedia.org/wiki/Dot-com_bubble), where equipment manufacturers lent money to their own customers just to book it as revenue growth. To a certain extent the same happened simultaneously across many industries as the dot-com bubble inflated, and the fibre bubble was just a very tangible example of that. "Casual Finance" in their video above also point to many other examples from previous centuries even proving that this is nothing new.

Coined by legendary investor [Sir John Templeton](https://www.investopedia.com/terms/j/john-templeton.asp), the ["four most dangerous words in investing"](https://www.investopedia.com/terms/t/this-time-is-different.asp) are: *"This time it's different."* Believing the current economic cycle is uniquely exempt from historical laws often leads to ignoring risk and repeating past financial bubbles.

So what evidence of a bubble do we have?

* Over-allocation of capital
* Artificial circular demand (vendor financing)
* Severe GDP distortion — in the US, but since the rest of the world uses mostly US tech, it's a number that must be kept in mind globally.
* Running an LLM business has never been profitable, and the situation is deteriorating rapidly. We are already seeing price hikes and token limits applied across all forms of LLM usage, except local models
* Unsustainable user retention costs / exploding marketing costs
* All tech stocks right now are "priced to perfection" and markets are hyper-sensitive. Even a small re-alignment [like the one from Broadcom](https://finance.yahoo.com/markets/stocks/article/broadcom-could-be-headed-for-one-of-the-worst-1-day-destructions-in-shareholder-value-ever-121457875.html) can trigger a meltdown. Guidance from Broadcom around a "few hundred million" shortfall triggered a violent reaction that wiped $300 billion from its value in a single session

To add insult to injury in addition to the, let's say, "logical" evidence above we also have several physical world constraints at play that can't be solved by just throwing more money (dump investments) at the problem.

* We can't expand physical infrastructure as fast as the current boom would require. Data centers require the buildings, but they require also supporting infrastructure. Power grids are already near capasity and sometimes even at over capasity. You simply cannot add more datacenters to that grid.
* Building new grids takes time as its a long process and once you have these new grids there is not enough power generation available to feed them.
* And building power plants are extremily high investment, long delivery time projects. So to get your new shiny data center a lot needs to happen before you can actually use it to host the GPUs you need. Or you can just [lease an nuclear power plant](https://www.theguardian.com/us-news/2025/nov/19/three-mile-island-nuclear-loan-microsoft-datacenter) I guess.

Laws and regulations are usually also slow to appear, but they have appeared. There are several constraints put in place or are soon coming into effect that set reins on how you can run your AI business. Cyber Security, immaterial right concerns and personal information security issues are on the minds of the regulators right now and deservably so. These regulations will understanably so hinder the profit growth (even more so) of your business if you are an AI provider leading to even higher barriers for new investment entry.

It's a powder keg waiting to explode, implode, and leak — all simultaneously as nothing is on stable ground.

## Final words

AI and LLMs are not going to go away. They are genuinely powerful tools when applied correctly, but the way we are currently using them — voluntarily and involuntarily — is not sustainable. It's a mirage of efficiency and, because of economic reality, the mirage will fade. What comes after this lunacy ends and the bubble burst will tell us how we actually will be using LLMs in the future. I argued previously that we will see the use move from the cloud to local devices where most of the work is done on local GPUs, TPUs and GPUs, but all extremily sofisticated work will still be requested through MCP by the local models from the cloud. The thing is that the compute on the cloud will become more expensive and will have an actual market value that makes profits for the service provider instead of loosing money like they currently do. And as Jevons Paradox tells us this will close the loop and cut the cycle as demand will go down. The cycle may begin anew when we start to optimize for the local LLM models to keep costs down, but the current cycle will die off taking the dump money and active investment bubble on a ride with it.

The Capital Cycle historically resolves in one of two ways: a slow bleed, where costs outrun revenues until players quietly exit, or a sharp trigger event — a high-profile bankruptcy, a massive earnings miss, or a credit event. Given how concentrated and circular current AI financing is, a **sharp trigger** is more probable than a slow bleed. Watch for: a major hyperscaler (Microsoft, Alphabet, Amazon, ...) publicly pulling back capex guidance, or a single large LLM vendor (OpenAI, Anthropic) announcing even more unsustainable burn rates. Either will puncture the circular demand illusion almost immediately.

Jevons tells us the intelligent use of intelligence will survive whatever comes next. Capital Cycle tells us a lot of the current players won't.
