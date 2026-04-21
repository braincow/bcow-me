+++
title = "What the LLM future will look like?"
weight = 0
updated = 2026-04-21

[taxonomies]
tags = ["llm", "ai", "technology", "opinion"]

+++

## Artificial intelligence it is not

Lets get the obvious thing out of the way: No, its not intelligent. AI as we currently know it is a next word guessing algorithm. More context just makes more educated guesses based on some randomness and larger pool of words to guess from based on how often they appear in conjunction with already previously guessed words. The more context and the larger model (more trained words aka better next guesses) just eat more cpu, gpu and memory resources globally while prompted, but there is a cost associated for training these new models too. 

AI can produce excellent language and be VERY convincing in its output, but looking more closer at it - it becomes clear that it is just theater performance for us. Back in the 80 you could get the same excitement from talking to an Eliza bot. Eliza was distributed at the back of magazine as BASIC code listing that you meticulously typed into your Commodore 64 BASIC prompt. Eliza too was very convincing at times too although it was a much simpler illusion than the current LLMs perform for us. Its algorithm also had nothing to do with current LLMs though, but the outcome was the same. And we as a species are also a really gullible bunch of monkeys making this possible - we believe the illusion so easily. Even a simpler bot than Eliza that I wrote back in the day that sat on IRC channels and just randomly insulted people or their Internet provider based on the users identity string was able to fool channels worth of people for hours and in the end get banned - not for being a bot, but because it was rude, obnoxious and generally toxic conversationalist.

So the intelligence is relative term here. More than anything we are willing to accept it as intelligence what LLM models output for our eyes to see which tells us more about ourselves than about the artificial intelligence models we use.

## Current hell scape

Startups. Venture capital. Hype. Faster news cycle with nonsensical updates on things that actually don't matter at all, but seem so relevant currently regardless.

Now where have I heard and seen this before? We are quickly replicating the conditions we had back in the early 00s and -07 with dot com bubble and the financial crisis. There  is a bubble now too which you can see with your own eyes and feel as that growing anxiety in the back of your mind that you cant quite express  what it is all about. Its about mass hysteria. Thats what it is all about.

We are collectively under the illusion that something HUGE and TRANSFORMATIVE is going on. No its not. What we actually are seeing is a hype cycle feeding a bubble and, thank god, its starting show signs of finally dying off.

NVIDIA sells nonexistent chips to OpenAI with money that does not exist into datacenters that have not yet been built and Microsoft buys models and "knowhow" from OpenAI for money they dont have. Everything is an illusion - money doubly so. When you see a news head line that states there is going to be a such and such deal with so much more billions it is important to remember that the billions dont actually exist as money - they are promises and intents of money. And when you pump non-existent currency into non-existent product well that is the definition of a bubble. Same happens with Google and others too, but maybe in a more less transparent way as Alphabet builds their own chips with their own money and does the research & development and products with their own money, but dont be mistaken the non-existent money flows there as well between columns of an accounting software somewhere. Google Cloud Next 2026 is right behind the corner and the AI this and AI that hype seems to override any actual value propositions in that conference program as well. Oh, I am a Google Cloud guy and think their tech is excellent, even best on the market, but still I consider this AI centric hype being a dangerous distraction. We have already seen this where API keys (that previously were not secrets) can suddenly be used by "hackers" to exploit Vertex AI if your API keys are not properly scoped; Which they were not as they were not previously considered to be secrets!

We are also training new models still with the same methods we did just few years back. Take in the overall "knowledge" of man kind in the Internet and feed that to the models prediction algorithm so that it can extrapolate the next possible word or piece of information that goes towards result of the users prompt. Now this model is broken. The Internet is filled with AI generated slop that gets feed into the models during training and we are starting to see the models degrade in quality while simultaneously gaining diminishing returns on what it cost to get the result from these models.

The fundamental issue of LLMs models has been hallucinations aka when the model does not have the information readily available or the context does not "allow" retrieval of the information it has due to that word having a smaller predictive score. This creates dangerous situations where models tell the users to eat soap or attempt suicide or do other completely idiotic things, but since they are very convincing in their verbal output and are usually polite while instructing the users we gullible monkeys do what we are told to our own peril. Even if the hallucination is not dangerous but obviously wrong in factual content then if that generated output is then published back to the Internet and then retrained back into some model we get even more chance for that wrong information to be retrieved next time by the model and returned as an answer to the user when prompted.

This is not a problem of adoption like a model would tell you; We are adopting alright. We have adopted so much AI capabilities into products where they are useful and even more so on products that have no place for AI assisted features. Since the adoption is so large this has created a problem to regulators. Where is the data stored? Does it contain personally identifiable information? Should there be some antitrust measures in place to protect consumers from big tech? What are the private security and corporate security implications of this technology? These things are still being debated and everyone is in a such a hurry to adopt that the risks are not properly evaluated.

## Burst

This situation is going to get worse before it gets better. Already Microsoft has started to refuse paying for OpenAIs nonsense and Alphabet had to go to the banks to get some capital in addition to their own deep pockets.

Also since USA is conducting an illegal war at Iran right now which has on its own increased inflation and energy costs in overall it has also disrupted the crucial supply of helium that is used in semiconductor manufacturing. This will also increase the price of datacenters and servers running AI models indirectly. Even before this latest hit the business model was not sustainable and now it is even less so.

The signs are there if you know how to read them. Token limitations have gone into effect on many services. Startups dont get money anymore by just pitching "AI enabled" keyword. Github Copilot has stopped temporarily on-boarding new customers. Google Gemini payed subscriptions for consumers have started to increase in price and gpus have ran out of some cloud provider datacenters preventing software companies from creating their own AI enabled features.

So the bubble is going to burst. If you allow me to play Nostradamus here I say it will happen on Q4 of 2026 or Q1 of 2027, but lets see. It will start from freezing or cancellation of AI infrastructure investments aka new datacenters and servers for running said models. When this happens the markets will recalibrate and the bubble bursts. Suddenly the value of non-existent services and goods disappear from the economy overnight, but the loans still have to be payed in full. There are going to be bankruptcies, mergers, layoffs and shutdowns of product lines - physical and electronic.

## What comes after?

While I still have the Nostradamus cloak on let me continue a bit more. After the bubble bursts do we return to the time before LLM and ChatGPT2.5?

Yes and no.

No because LLMs are useful tools in certain scenarios that has been proven, but will use them differently. Yes because not everyone can afford the use them like we currently do.

LLMs will move to on our phones and other end point devices like laptops, but what we will be running are more restricted models like Gemma or Mistral. These endpoint models will then connect to more advanced, purpose built, high-powered models over MCP protocol that are running in the cloud and we will pay for the cpu, gpu and memory used based on a "hourly rate". So suddenly feeding your entire program code as context to ask the model to move your button three pixels to the right is no longer a viable prompt for a developer. Local models also solve the sovereignty and data security issues we currently have. As we control the model runtimes and can dictate where they are stored in, what gets stored in them and where any processing or data storage in general takes place we can enforce same security frameworks on them as we currently do on software on our phones or corporate endpoint devices such as laptops.

As LLM models become expensive to prompt at market prices this means that the professions that we "lost" to the hype will get their jobs back because nothing beats the good old human brain and a human computer interface known as the keyboard and mouse - and or a stylus.

LLMs will in the end fulfill the promise that we were sold during all this hype: it will increase productivity, but without all the nonsense and the tooling is priced according to its usefulness and how much it actually costs to use.

Im tired. I just want this hype to die down so that we can start the cycle again with the next thing - what ever that might be. I just hope that it will be something which does not affect my professional landscape so that I can look out of the window and not see everything on fire and just wonder to myself "why are those people in panic and running around in circles while cursing out loud?". Ignorance is a bliss.
