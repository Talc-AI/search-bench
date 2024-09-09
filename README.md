# SearchBench

There's a number of academic performance benchmarks for LLMs, but there are two major issues that prevent benchmarks from being useful to real product teams

1. They're static. Because they leak everywhere they're easily gamed and overfit. Even if unintentional, static benchmarks inevietably make their way into training data.
2. They're laregly theorhetical. They have an extremely academic focus on the theorhetical limits of LLM capabilities, and reasoning. As a result, feedback from standards like MMLU often don't give us much information about how a product works. What are you supposed to do if your AI doesn't answer a MCAT question correctly? Do your users even care? 

We wanted to make a practical benchmark that focuses on every day helpfulness of these search assistants. 
Searchbench is a benchmark of realistic queries and expected answers with the goal of giving timely and tangible feedback to product teams.

## Methodology

#### Dataset Creation

Our service, Talc, turns knowledge bases into Q&A datasets for testing and training. At a high level, we:

1. Scrape various trustworthy sources for interesting facts and lessons
2. Create sets of Q&A to represent those facts
3. Adjust the tone, style, and distribution of those queries to best match production users as we can. (There are obvious limitations to customization here)

We used our pipelines to generate thousands of example Q&A, and filtered it down manually to the highest quality, most interesting 900 samples.

#### Query Categories

We have 4 major buckets of queries we've put into SearchBench. Each of these attempt to mimic realistic day to day usage of these products.

1. Name

Description

2. Name

Description

3. Name
 
Description

5. Name

Description // Notably, we update this section regularly with the latest news, la la la. 
This means that Searchbench isn't always comparable across points in time; we will update this regularly. Our goal is to give product feedback, so it's more important for a product to keep up with the latest news than it is for our benchmark to be static.

#### Tradeoffs

Because search answers are often given in different formats across different products, we use LLMs-as-a-judge to evaluate their efficacy. We believe that this results in a more representative test than standard multiple choice style benchmarks.

There are limitations to this; particularly that different products might believe different answer formats are "better" than others.
We don't make major attempts to discern between the subjective quality of answers beyond factual accuracy and relative conciseness.

In addition, we acknowledge that LLMs-as-a-judge, though relatively effective, may sometimes make mistakes. This would an issue for an academic benchmark where rigor and leaderboards are prioritized but this is not a benchmark for academics; it is for product builders.

It's impractical for teams to manually test 1000 questions at a time every time they push a new PR; dev teams need relatively informative feedback quickly. With SearchBench we are OK with a few false positives if it means that teams get fast day to day feedback on how their changes.

## Moving Forward

You can expect us to update this benchmark from time to time to keep up with the latest going on in the world! We're also very open to feedback; this benchmark is by no means perfect, and should not stand static through time.

If you find things are wrong, we'll correct it. If you find questions are unhelpful or irrelevant, let us know what would be more helpful and we'll add it. 

Searchbench isn't an academic gold standard; it is a practical, thorough-as-can-be feedback tool build for the people who care more about their users than leaderboards.




