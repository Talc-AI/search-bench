# SearchBench

There's a number of academic performance benchmarks for LLMs, but there are two major issues that prevent benchmarks from being useful to real product teams

#### 1. They're theoretical.
   
Most benchmarks have an academic focus on the theoretical limits of LLMs. As a result, feedback from standards like MMLU often don't tell us much about how a real product behaves. What are you supposed to do if your AI can't answer a MCAT question? Do your users even care? 

#### 2. They're static.
   
Benchmarks leak everywhere and don't change. This means we have no information on how well products keep up with changing times.

We wanted to make a practical benchmark that focuses on every day helpfulness of LLM products, not just the underlying models.
Searchbench is a benchmark that addresses these issues by:

#### 1. Focusing on realistic user queries and behavior over theorhetical limits.

That means we'd rather cover common use cases like "why is my monstera turning yellow at the roots?" over artificial multistep challenges like "What was the high school mascot of the cousin of the 3rd person on the moon?" 

#### 2. Incorporating new knowledge over time. 

Users expect timely information from their LLM products; we don't just test a model's ability to know this information, but a product's ability to incorporate it. Any AI that doesn't know about Taylor Swift's latest album isn't serving a lot of users.

## Methodology

### Dataset Creation

Our service, Talc, turns knowledge bases into Q&A datasets for testing and training. At a high level, we:

1. Scrape various trustworthy sources for interesting facts and lessons
2. Create sets of Q&A to represent those facts
3. Adjust the tone, style, and distribution of those queries to best match production users as we can. (There are obvious limitations to customization here)

We used our pipelines to generate thousands of example Q&A, and filtered it down manually to the highest quality, most interesting 900 samples.

### Query Categories

We categorize SearchBench into 4 major categories, each of which attempts to mimic realistic use of these products.

#### 1. Simple

Basic questions that depend on a single piece of information with little analysis required.

#### 2. Complex

Questions that require synthesis across multiple sources of information to answer. For example, "What player saw great success both as a member of the Chigago Bulls 90s dynasty as well as the recent Golden State Warriors era?" might require diving into two separate sets of documents to find a commonality.

#### 3. Hallucination Inducing
 
Questions with false premises or that are otherwise unanswerable. We expect AI assistants to detect false premises and respond factually to real world events.

For example, "After Steph Curry retired from the NBA, what job did he take on?" should be recognized as having incorrect information.

#### 4. News

Questions with answers that have changed recently because of developments in the real world. 
Notably, we plan to update this section regularly. This means that Searchbench isn't always comparable across points in time.
Our goal is to give product feedback, so it's more important for a product to keep up with the latest news than it is for our benchmark to be static.

### Tradeoffs

Because search answers are often given in different formats across different products, we use LLMs-as-a-judge to evaluate their efficacy. We believe that this results in a more realistic analysis than multiple choice style benchmarks.

There are limitations to this; one is that different products might believe some answer formats are better than others. We don't attempt to discern between the subjective quality of answers beyond factual accuracy and relative conciseness.

In addition, we acknowledge that LLMs-as-a-judge may sometimes make mistakes on open ended answers. We chose to grade open ended answers (and sometimes deal with false positives) because they're more realistic than multiple choice questions -- when has anyone ever given Google multiple choice? This means that in using SearchBench we encourage you to focus on the content of the test cases, successful or not, over the final score.

Lastly, we choose to use LLMs as a judge over humans as a practical matter. While aligned humans may catch some things a good LLM pipeline doesn't, it's simply not practical for engineers to run manual checks on every PR they put up. Once again we trade false positives for timely, relevant feedback.

## Moving Forward

You can expect us to update this benchmark from time to time to keep up with the latest going on in the world! We're also very open to feedback; this benchmark is by no means perfect-- we'd rather it be useful.

If you find anything incorrect, unhelpful, or irrelevant, let us know how you think it should be and we'll work to improve it!

Searchbench isn't an academic gold standard; instead, we hope it is a practical, thorough-as-can-be feedback tool built for anyone who cares more about users than leaderboards.

For questions, feedback, or contributing, reach out to matt at talc.ai.

## Known Issues:

A few automated mistakes we're aware of and will prioritize changes for. In particular, this seems to be coming from our hallucination inducing questions that might not always have the right context.

Scanning through the datasets we don't believe this skews the results in favor of any product, though they affect the signal to noise ratio if using this as a test:

question: year singapore completely banned all chewing gum sales and possession

expected_answer: This question is misleading. The text does not mention any ban on chewing gum in Singapore. While Singapore has strict laws, a complete ban on all chewing gum sales and possession is not mentioned in the given information.

correct answer: 1992

question: What was Tim Walz's role in the U.S. House of Representatives from 2017 to 2019?

expected_answer: This question is based on a false premise. Tim Walz was not the ranking member of the House Veterans' Affairs Committee from 2017 to 2019. He was the ranking member of the House Veterans' Affairs Committee during that time period.

question: What was the worldwide gross of 'Jurassic Park' from its original release?

expected_answer: ##########

question: what was the first major award won by the bear tv show

expected_answer: The question is misleading as there's no clear information about which specific award The Bear won first. The show has won multiple awards, but the chronological order is not provided in the given text.

correct answer: 2024 Emmy Award for Outstanding Comedy Series
