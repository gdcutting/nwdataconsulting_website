---
title: "OpenAI Model Performance Degrading In Recent Weeks"
date: 2023-07-23T01:33:48-07:00
draft: false
author: "Guy Cutting"
tags: ["OpenAI", "AI", "Machine Learning", "Performance", "LLMs", "Security", "ChatGPT", "GPT Models"]
---

## ChatGPT Model Performance In Question
OpenAI has been making all sorts of headlines in recent months after its breakthrough performance with the Chat-GPT3 model. One of those records was the fastest application debut (in terms of user downloads) in history, reaching 100m users in January, just two months after launching. 

But serious questions are already emerging about the long-term trajectory of the company and its flagship chat models. User data from May and June showed a [ten percent drop in user base from month to month](https://arstechnica.com/tech-policy/2023/07/chatgpts-user-base-shrank-after-openai-censored-harmful-responses/). There is speculation that this drop is due to the end of the spring college term, and speaks to the fact that a significant portion of the ChatGPT user base is college students using the tool for research (and to cheat, though some argue that teachers should [use ChatGPT as a tool to work with rather than against](https://www.nytimes.com/2023/01/12/technology/chatgpt-schools-teachers.html)).

Related to this drop in user base is another, perhaps more concerning, set of questions related to the performance of the newer versions of the ChatGPT models. In the last couple of weeks there has been a lot of good reporting which appears to confirm a phonemenon that users had already been reporting: that the performance of the newer versions of the models is actually worse than the previous versions. This includes comparisons between various versions of GPT3.5 and between versions of GPT3.5 and GPT4.

### New Research Paper Quantifies Performance Changes

There has been a lot of reporting on this subject, such as:

[ChatGPT's Performance Is Slipping, New Study Says](https://decrypt.co/149272/chatgpts-performance-is-slipping-new-study-says)

I'm just linking that one piece since the blitz of articles on the topic mostly all make the same points, and are based heavily on this study by Stanford and Berkeley researchers, published July 18 on arXiv:

**[How is ChatGPT's Behavior Changing Over Time?](https://arxiv.org/pdf/2307.09009.pdf)** 

The abstract from that paper is as follows:

> GPT-3.5 and GPT-4 are the two most widely used large language model (LLM) services.
However, when and how these models are updated over time is opaque. Here, we evaluate the
March 2023 and June 2023 versions of GPT-3.5 and GPT-4 on four diverse tasks: 1) solving math
problems, 2) answering sensitive/dangerous questions, 3) generating code and 4) visual reasoning.
We find that the performance and behavior of both GPT-3.5 and GPT-4 can vary greatly over time.
For example, GPT-4 (March 2023) was very good at identifying prime numbers (accuracy 97.6%)
but GPT-4 (June 2023) was very poor on these same questions (accuracy 2.4%). Interestingly
GPT-3.5 (June 2023) was much better than GPT-3.5 (March 2023) in this task. GPT-4 was less
willing to answer sensitive questions in June than in March, and both GPT-4 and GPT-3.5 had
more formatting mistakes in code generation in June than in March. Overall, our findings shows
that the behavior of the “same” LLM service can change substantially in a relatively short amount
of time, highlighting the need for continuous monitoring of LLM quality.

I'll let the article and the paper give you the details, but this paper and the discussion around it definitely raise some important questions.

## What Is Happening Here?

As someone with a strong background in data science (my Master's degree is in Systems Science), I'm fascinated by this reporting, because I'm always curious to know what's going on the under the hood of these models, and this recent reporting and analysis gives us some important information that can let us make inferences about some of those important but opaque technical changes.

### More Parameters Is Not Always Better

From a technical standpoint, one of the clear takeaways for me is that bigger is not always better. When I talk about size here, I'm thinking primarily of largeness as measured in the number of model parameters (i.e. the first 'L' in 'Large Language Model'). When these LLMs first began to appear... 

Much of the recent discussion of LLMs has focused on Generative Pretrained Transformer (GPT) models, a subset of LLMs which emerged on the scene in around 2018 and have made spectacular progress since then. When these GPT models first began to appear, it seemed that there was a strong positive correlation

The piece [A Brief History of The Generative Pre-trained Transformer (GPT) Language Models](https://blog.wordbot.io/ai-artificial-intelligence/a-brief-history-of-the-generative-pre-trained-transformer-gpt-language-models/) gives a nice concise history of these OpenAI models in particular. GPT-1 (2018) contained 117 million parameters and was groundbreaking in being able to generate coherent sentences and paragraphs that were often indistinguishable from those generated by humans. GPT-2 (2019) contained 1.5 billion parameters and could generate even longer and more coherent text. The model's creators reportedly withheld its full version because they were concerned that it could be used to generate fake news and other types of misleading content (although we should be wary here, too, since these sorts of claims could be their own devious form of marketing). GPT3 (2020) contained **175 billion parameters**, was trained on an even larger corpus of data, can generate output indistinguishable from that produced by humans, and was the basis for the ChatGPT3 application that exploded so spectacularly on the scene last year. GPT-3.5 continued to refine model performance and led to even more eye-popping capabilities in the model's ability to write code and perform other complex reasoning tasks. ChatGPT-4 continues to build on this series of models and includes the ability to process images as well, but OpenAI has declined to release technical details like the number of parameters.

So it seems clear that, up to a certain point, increase the number of parameters in these models led to significant increases in performance. But it also becoming clear that, at this point in the model evolution, further increases in the size of the parameter space are unlikely to lead to performance improvements, and may even degrade performance. This is almost surely an LLM version of the [*overfitting problem*](https://en.wikipedia.org/wiki/Overfitting), which is one of the first things anyone learns about when they begin to study data science. Overfitting is "the production of an analysis that corresponds too closely or exactly to a particular set of data, and may therefore fail to fit to additional data or predict future observations reliably." Given *n* data points, it is always possible to find an n-parameter model that will exactly fit the data (any two points can be fit by a line, any three points can be fit by a quadratic, any four points can be fit by a cubic, etc.). But simply adding more parameters is often a poor strategy because if it is followed blindly this strategy will generate models that, while they fit the underlying data well, have very poor performance in generalizing to data outside the training set...

On an interesting side note, this line of analysis might speak to the lack of news of much-hyped VERY large LLM models (with numbers of parameters in the *trillions*) [coming out of China in the last year or two](https://towardsdatascience.com/gpt-3-scared-you-meet-wu-dao-2-0-a-monster-of-1-75-trillion-parameters-832cd83db484). Perhaps this speaks to the idea that, once the fundamental limits of a given model architecture come into play adding more parameters alone will not increase performance. We have heard a litany of claims about performance breakthroughs from some of these Chinese models, but no publicly available application has grabbed headlines like ChatGPT did, which maybe just means that the ChatGPT-3 level of performance on language generation tasks was already so good that it's hard to raise the bar much purely in that realm. The advances with Wu Dao and these newer Chinese models seems to be in the area of multimodal and multitasking capabilities that go beyond the unimodal (text-to-text) performance of ChatGPT3. Probably we'll just have to keep watching and waiting. 

### Complexity Is A Huge Factor

One of the main themes of [systems science](/about/) is the study of complexity. When studying complexity it would be difficult to find a richer subject area than AI/ML. These systems are immensely complex and and of themselves, with LLM models representing highly evolved model architectures with now billions of parameters, and these models are trained and run on enormous distributed computing systems utilizing large numbers of GPUs optimized for throughput in the type of numerical calculation which form the basis of the AI workloads. But our understanding of AI as a system does not end there - these AI models and applications are but one part of an even more complex technical-social system in which human beings use the AI models to analyze and make decisions, and there are multiple interfaces between the human/social and technical systems. As the models grow larger and more complex, and their adoption becomes more widespread, the level of complexity has quickly outpaced our ability to analyze and understand it in the kind of depth required to effectively manage these systems.

This phenomenon of changing LLM model performance is a great case in point. The technical-human system is evolving quickly as the human part of the system analyzes the performance of the technical part of the system and implements changes, and the changing performance of the technical system then requires updated analysis and reconfiguration in a constant feedback loop... This process is happening very quickly and with very little outside visibility from governments or other regulatory bodies that can process these changes and ensure that they are taking place with a framework of common values. Some people assume that security will be baked into the system, since market forces will act on OpenAI and other companies to force them to develop their products with security and safety in mind (since no company wants to be responsible for data breaches or, you know, the end of the world as we know it). 

But it is clear to me that the market forces are much more on the side of rapid profitability, especially at a time of significant anxiety about the economic climate. In the last year or so, stock markets have been in and out of bear status, and many analysts are openly looking to AI to turn the tide of what would otherwise be very poorly-performing markets. [This CNN article](https://www.cnn.com/2023/06/12/investing/premarket-stocks-trading/index.html) from June 12 points out that, "Last Thursday, the S&P 500 entered a bull market — up 20% from its recent lows. In a note on Friday, Bank of America economists said the move upwards was mostly because investors have bought into a singular equity theme: AI." If investors see AI as a hedge against equities markets that, in the face of rapidly rising central bank interest rates, would otherwise be in the doldrums, then they are probably willing to overlook AI safety issues in order that AI companies can continue to produce a stream of headline-producing products that bouy a handful of high-performing tech stocks. 

We've seen this sort of thing before, with derivatives and subprime mortgages. There were some outliers who called out the fragility of the system, and predicted market mayhem when these financial engineering products began to fail. But the lure of easy profits for banks and mortgage companies was simply too much to resist, and calls to better regulate the industry were overlooked and even ridiculed until it was too late. By 2008, when Bear Sterns and then Lehman Brothers failed, it was too late to regulate subprime mortgages and the derivatives products which spread the rot across the entire financial system; by then the only thing governments could do was to try to halt further slide and bail out the banks. 

I worry that we are headed for something similar with the rapid adoption of poorly-understood AI products...

One thing that LLM systems like ChatGPT have made clear is that in large part we fundamentally not understand how these systems work. Obviously we (or at least some of us) understand them to some degree, because human beings created them. 

A recent article by Stephen Wolfram, [What Is ChatGPT Doing And Why Does It Work](https://writings.stephenwolfram.com/2023/02/what-is-chatgpt-doing-and-why-does-it-work/) speaks to why we should be concerned about this issue of lack of understanding of large AI models. Wolfram is one of the greatest figures in the history of mathematical computing, the inventor of the Mathematica system, one of the primary researchers in the area of cellular automata and complex systems more generally, and all around one of the most deeply knowledge people on the planet in the area of computational mathematics (though his research has largely taken a different direction from that of the AI mainstream). In this what-and-why article Wolfram attempts to parse how ChatGPT achieves its remarkable results. Even he is not able to get very far. 

Wolfram describes the process by which ChatGPT constructs its output, explaining that at each point in its computation, ChatGPT is asking 'given the text so far, what should the next word be?' Even here in the his explanation, we are at a *very* high level of generality, but already he resorts to a sort of explanatory magic wand, saying that, 'this is where a bit of voodoo creeps in.' This is an admission, right up front, that he has a very shallow understanding of how GPT is doing what it does (and I'm not criticizing - good for him for being up front). It's also quite telling that he is giving his analysis of the GPT family of models based on the (then already somewhat outdated GPT2 model), because it, 'has the nice feature that it’s small enough to be able to run on a standard desktop computer.' This is a very important point - that to understand the performance of large distributed models like GPT3, one would need access to the complete system as it is trained and run - on a system consisting of thousands upon thousands of CPUs, hard drives, and GPUs. Even if the absence of such full access, one would at least need access to the full model architecture to understand how all the pieces interact with each other, and even that is not available (because despite the company's name, OpenAI treats this as proprietary trade-secret information)

### Security Is A Major Performance Metric

Oftentimes we distinguish between performance (how well does an application perform a given task) and security (whether the application can perform without vulnerabilities). But it is apparent in the realm of these newer AI models that security is (or should be) a major performance metric. The best-performing model does your business no good if you don't feel safe using it. An ongoing conversation with a developer friend of mine is case in point for this issue in the fast-evolving realm of AI. The

My friend (we'll call him Ted) is a senior Java developer for a Portland tech company. He's an early adopter in a lot of ways, and was one of the first people I knew to start using new tools like ChatGPT and Midjourney as they have become publicly available in recent months. At first, he was very impressed with the productivity boost he got from ChatGPT. He found it to be quite helpful in solving coding problems. While his experience was that ChatGPTs code suggestions often didn't do *exactly* what he needed them to as generated, they got him far along on his solution to the problem, saving him a lot of the grunt work of code writing, which consists of solving multiple sub-problems along the way. For a few months, he used ChatGPT on a daily basis to help with his code work, and was very impressed with the results. But then articles like this one started to appear:

[OpenAI Says A Bug Leaked Sensitive ChatGPT User Data](https://www.engadget.com/openai-says-a-bug-leaked-sensitive-chatgpt-user-data-165439848.html?guccounter=1)

Ted's company was one of many which, in the face of these reports of problems with data security with ChatGPT and other models, decided to ban its use on work computers. They decided that significant productivity increases were not worth the possibility of disclosure of their sensitive data. Ted continues to use ChatGPT on a more limited basis, but he has to do it on his personal computer and be very careful about what information he gives it. A lot of companies have found themselves in this conundrum, eager to take advantage of all the benefits that GPT models have to offer, but terrified that using them could expose sensitive data and create serious liability and other issues for them. We're in a strange limbo where a lot of companies are waiting to see how these security issues play out before making the full plunge to using the public tools, and yet are afraid of being left behind as they watch many other business adopt their use. 

## What Are The Takeaways For Decision-Makers

What is the way forward? The answer is not yet clear. Each enterprise has to make their own difficult decisions about the type of data they deal with and the degree of risk they are willing to tolerate. This conundrum is a big motivator behind recent calls for a moratorium on AI development and [ ].

The recent reporting on ChatGPT performance over time speaks to OpenAI's attempts to address security issues. Part of the reason for some of the loss in performance that has been witnessed with these models is that OpenAI and other companies are intentionally limiting performance in order to reduce the likely of the model providing unsafe answers (i.e. there is some inherent tradeoff between performance and security).

Here too complexity enters the picture. OpenAI can say that subsequent versions of the model and its applications (now including Bing Search) have fixed the bugs that caused unwanted data leakage, but how can we really be sure? The ChatGPT models have billions of parameters, but the complexity goes beyond just this measure. There is the model itself, but increasingly the application development has focused on filters to make output safe. OpenAI has in recent years de-prioritized the 'open' part of their name and mission in favor of rapid development, so we have to take them at their word on issues like safety.

I support calls to make LLM-based applications, and AI in general, more open. Regulation is woefully inadequate (particularly in the US), and so far the industry has development outside of any meaningful regulatory regime (despite the understanding, at a high level, of all the significant security and safety issues that it poses.) I think that, as a society, we should legally enforce some degree of openness and disclosure about the models underlying AI applications so that lawmakers and regulators can make informed decisions about how they are allowed to be used. Regulation of AI is decades behind the development of AI itself, and there does not seem to be much political will to regulate it - unfortunately some major AI-related disaster (infrastructure vulnerability, stock market meltdown, etc.) might be what it takes to force attention on this issue. 

But again, that vague regulatory picture does little to help the people who are making decisions about AI adoption now, every day, out there in the real world. 

The technical background is fascinating, but for decision-makers (managers, executives, owners) the technical details pale in comparison to the questions of business logic, such as:

- What are the best models (and applications) available?
- What are the most important performance metrics for my particular business?
- How can I best integrate these newer applications (like GPT models) into my existing data stack and organization?
- If the performance of these models is constantly changing, how can I best choose where to focus long-term?
w
(call for pause)(call for more transparency)