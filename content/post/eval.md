+++
title = "What's wrong with LLM Evaluation?: Evaluation is Hard (& also Costly)."
date = 2019-01-25T00:00:00
+++

Language models are trained with millions of dollars, involving very intricate engineering jobs, as well as thousands of hours of manpower and human stresses. However, day by day, the evaluation of language models is becoming so confusing and cumbersome that it becomes almost impossible to confidently say which language model is better at what. In this article, I have tried to sketch out some of my observations and findings, provide some recipes, and conclude with a call for a more rigorous approach to language model evaluation.

## Table of Content

- [What makes a good evaluation suite for leaderboard?](#what-makes-a-good-evaluation-suite-for-leaderboard)
	- [Evaluation Benchmarks](#evaluation-benchmarks)
		- [NLP Tasks](#nlp-tasks)
		- [Programming Language Tasks](#programming-language-tasks)
	- [What to Evaluate?](#what-to-evaluate)
	- Explainability of the evaluation outcome?
- Performance indicators
	- Pretrained Language Model evaluation vs ChatModel evaluation
	- The confusion on rank based evaluation and generative evaluation
	- The irony of generative metrics?
	- The True Generative Evaluation?
- When evaluation should be automated and when human in a loop?
- Metric learning
- Evaluation bias, Can (& When) LLM-evaluation be a good indicator?
- Example of an ideal evaluation scenario?
- A call for more rigour evaluation
	- Total number of vocabulary covered?
	- Total number of domain covered?
	- Training token vs Evaluation token
	- Use of a common prompting framework
	- Share Inference Outputs
	- Evaluation hyperparameters
	- Few-shot vs Zero-shot evaluation
	- Prioratizing manual evaluation (author vs independent evaluation)
	- Avoid Anthromorphizing
	- Whom to credit?
- Evaluation is not solved
	- Multi-hop testbed
	- Agentic evaluation

**Prerequisites**: I assume the readers have the following knowledge:
- The currect tide of LLM evaluation crisis.
- Interaction with one or more LLM in form of `ChatModel` (i.e., `ChatGPT`, `Vicuna`) and pretrained model (i.e., `T5`, `GPT-J`, `GPT-3`)

## What makes a good evaluation suite for leaderboard?

NLP community has been obssessed by leaderboards. Before going to the discussions, lets list out some of the popular evaluation benchmarks and datasets with minimal statistics. (If the tables are too exaustive for you, please go ahead to the next section from the [Table of Content](#table-of-content))  

### Evaluation Benchmarks

#### NLP Tasks

 Here is a summary of a list of benchmarks NLP Tasks (in no particular order), 

| Benchmark - Task Type | Dataset | Split | No. of Samples |
| --- | --- | --- | --- |
| [GLUE](https://arxiv.org/abs/1804.07461) | | |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Grammatical Acceptability, NLU | [CoLA](https://arxiv.org/abs/1805.12471) | dev | 1043 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sentiment, NLU	  | [SST-2](https://aclanthology.org/D13-1170/) | dev | 872 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Paraphrases, NLU	  | [MRPC](https://aclanthology.org/I05-5002/) | dev | 408 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Paraphrases, NLU	  | [QQP](https://quoradata.quora.com/First-Quora-Dataset-Release-Question-Pairs) | dev | 40430 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Score 0-5 , NLU | [STSB](https://aclanthology.org/S17-2001/) | dev | 1500 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Natural Language Inference	  | [MNLI](https://cims.nyu.edu/~sbowman/multinli/paper.pdf) | dev | 19647 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Natural Language Inference, Squad.V1	  | [QNLI](https://arxiv.org/abs/1606.05250) | dev | 5463 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Natural Language Inference	  | RTE [[1]](https://cims.nyu.edu/~sbowman/multinli/paper.pdf) [2](https://link.springer.com/chapter/10.1007/11736790_9) [[2]](https://www.researchgate.net/publication/247999003_The_second_PASCAL_recognising_textual_entailment_challenge) [[3]](https://aclanthology.org/W07-1401/) [[4]](https://link.springer.com/chapter/10.1007/11736790_9)	 | dev | 277 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Natural Language Inference	  | [WNLI](https://cdn.aaai.org/ocs/4492/4492-21843-1-PB.pdf) | dev | 71 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Natural Language Inference	  | [AX](https://gluebenchmark.com/diagnostics) | test | 1104 |
| [SuperGLUE](https://arxiv.org/abs/1905.00537) | | | 
| Binary QA | [BoolQ](https://arxiv.org/abs/1905.10044) | Dev | 3270 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Natural Language Inference | [CB](https://ojs.ub.uni-konstanz.de/sub/index.php/sub/article/view/601)  | Dev | 56  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Causal Reasoning    | [COPA](https://aaai.org/ocs/SSS/SSS11/paper/view/2418) | Dev | 100 |
|  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Reading Comprehension (True/False)   | [MultiRC](https://aclanthology.org/N18-1023.pdf) | Dev | 4848 |
|  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Multiple-choice QA    | [ReCoRD](https://arxiv.org/abs/1810.12885) | Dev | 10000 |
|  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Natural Language Inference   | RTE [[1]](https://cims.nyu.edu/~sbowman/multinli/paper.pdf) [2](https://link.springer.com/chapter/10.1007/11736790_9) [[2]](https://www.researchgate.net/publication/247999003_The_second_PASCAL_recognising_textual_entailment_challenge) [[3]](https://aclanthology.org/W07-1401/) [[4]](https://link.springer.com/chapter/10.1007/11736790_9) | Dev | 278 |
|  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Word-in-Context   | [WiC](https://arxiv.org/abs/1808.09121) | Dev | 638 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Reading Comprehension with Pronoun    | [WSC](https://cdn.aaai.org/ocs/4492/4492-21843-1-PB.pdf) | Dev | 104 |
|  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Natural Language Inference   | [AX-b](https://aclanthology.org/D18-1007/) | Test | 1104 |
|  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Gender Bias	   | [AX-g](https://aclanthology.org/N18-2003/) | Test | 356 |
| [BIG-bench](https://arxiv.org/pdf/2206.04615.pdf) (Crowdsourced Massive Multitask) | [Task List](https://github.com/google/BIG-bench/blob/main/bigbench/benchmark_tasks/README.md) | Test | 214 task (not number of sample)|   
| [Big-Bench Hard](https://arxiv.org/abs/2210.09261) | [23 hand picked tasks from Big-Bench](https://github.com/suzgunmirac/BIG-Bench-Hard) | Test | 6511 |
| Humanities, Social Sciences, STEM etc.  | [MMLU](https://arxiv.org/abs/2009.03300)  | Test | 14042 |
| [Inverse Scaling Challenge](https://www.lesswrong.com/posts/iznohbCPFkeB9kAJL/inverse-scaling-prize-round-1-winners) | [11 tasks](https://github.com/jasonwei20/inv-scaling-prompts/) | CoT/Direct | 1808 |
| Ethics Benchmark | [5 subset of task,  Justice, Virtue, Deontology Utilitarianism, Commonsense](https://arxiv.org/abs/2008.02275)| Test/Hard Test | 19968/18604 |
| Open Domain QA | | | 
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Trivia QDQA | [TriviaQA (rc)](https://aclanthology.org/P17-1147/) | Dev | 17944 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Wiki QDQA    | [NQ-Open](https://arxiv.org/abs/1906.00300) | Dev | 3610 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Single Named Entity based ODQA    | [WebQuestions](https://aclanthology.org/D13-1160.pdf) | Test | 2032 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Subset of Wiki ODQA    | [EfficientQA](https://arxiv.org/abs/2101.00133) | Dev | 1800 |
| Reading Comprehension | | |
|   | [Race-Middle](https://arxiv.org/abs/1704.04683) | Test | 1436 |
|     | [Race-High](https://arxiv.org/abs/1704.04683) | Test | 3498 |
|     | [SQuAD-V2](	) | Dev | 11873 |
Common Sense Reasoning | | |
|  | [PIQA](https://arxiv.org/abs/1911.11641) | Dev | 1838 |
|     | [SIQA](https://arxiv.org/abs/1904.09728v3) | Dev | 1954 |
|     | [HellaSwag](https://arxiv.org/abs/1905.07830) | Dev | 10042 |
|     | [WinoGrande](https://arxiv.org/abs/1907.10641) | Dev | 1267 |
|     | [ARC-Easy](https://arxiv.org/abs/1803.05457) | Test | 2376 |
|     | [ARC-Challenge](https://arxiv.org/abs/1803.05457) | Test | 1172 |
|     | [OBQA](https://www.semanticscholar.org/paper/Can-a-Suit-of-Armor-Conduct-Electricity-A-New-for-Mihaylov-Clark/1536e8958697c5364f68b2e2448905dbbeb3a0ca) | Test | 500 |
| Mathematical Reasoning  | | |
| | [MATH](https://arxiv.org/abs/2103.03874) | Test | 5000 |
|     | [GSM-8k](https://arxiv.org/pdf/2110.14168v2.pdf) | Test | 1319 |
|     | [MGSM](https://arxiv.org/abs/2210.03057) | Test, 11 lang | 2750 |
| Natural Language Inference | | |
| | [ANLI R1, R2, R3](https://arxiv.org/abs/1910.14599) | Test | 3200 |
| | [MNLI](https://cims.nyu.edu/~sbowman/multinli/paper.pdf) | dev | 19647 |
| | [XNLI](https://aclanthology.org/D18-1269.pdf) | Test, 15 lang | 75150 |
| Text Summarization | | 
| | CNN/DM [[1]](https://arxiv.org/abs/1704.04368)[[2]](https://arxiv.org/abs/1506.03340) | Test | 11490 |
|     | [XSUM](https://arxiv.org/pdf/1808.08745v1.pdf) | Test | 11334 |
|     | [SAMSum](https://aclanthology.org/D19-5409/) | Test | 819 |
|     | [DialogSum](https://arxiv.org/abs/2105.06762) | Test | 500 |
| Bias and Misinformation | | 
|  	  | [Gender Bias](https://aclanthology.org/N18-2003/) | Test | 356 |
| 	  | [WinoBias](https://arxiv.org/pdf/1804.06876v1.pdf) | Test | 1580 |
|     | [TruthfulQA](https://arxiv.org/abs/2109.07958) | Test | 817 |
| Sequence Labeling | | 
| Named Entity Recognition | [CoNLL 2003 Shared Task](https://aclanthology.org/W03-0419/) | Test on 2 lang | 6458 |
| Named Entity Recognition | [CoNLL 2002 Shared Task](https://aclanthology.org/W02-2024/) | Test on 2 lang | 6593 |
| Named Entity Recognition | [Bari et al 2020](https://arxiv.org/abs/1911.09812) | Test on 2 lang | 3766 |
| Parts of Speech tagging | [Universal Dependencies 2.7](https://lindat.cz/repository/xmlui/handle/11234/1-3424) | Test on 2 lang | 5427 |
| Named Entity Recognition | [WikiANN](https://aclanthology.org/P19-1015/) | 473000 |
| XGLUE| | | |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Named Entity Recognition | CoNLL [2002](https://aclanthology.org/W02-2024/) [2003](https://aclanthology.org/W03-0419/) Shared Task | Test | 13186 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Parts of Speech tagging |  [UD 2.5](https://lindat.mff.cuni.cz/repository/xmlui/handle/11234/1-3105) | test | |
| XTREME | | |
| LinCE | | |
| GLUECoS | |
| GENIE | | |
| Long Arena | | |
| GEM | | |
| DialoGLUE | | |



#### Programming Language Tasks
And here is a list of programming language code evaluation benchmark taken from [MAM Khan et. al.](https://arxiv.org/pdf/2303.03004.pdf)

| Dataset                                                                 | Train      | Test    | La | Task Type          | Evaluation | Level   | Genre                    |
|-------------------------------------------------------------------------|------------|---------|----|--------------------|------------|---------|--------------------------|
| [Django](https://ieeexplore.ieee.org/document/7372045/)                                                                  | 16,000     | 1,805   | 1  | Program Synthesis  | Lexical    | Local   | N/A                      |
| [WikiSQL](https://arxiv.org/abs/1709.00103)                                                                 | 56,355     | 15,878  | 1  | SQL Queries        | Lexical    | Modular | SQL                      |
| [Antonio Valerio Miceli Barone et al](https://aclanthology.org/I17-2053/)                             | 109,108    | 2,000   | 1  | Synthesis, Summarization    | Lexical    | Local   | Github                   |
| [CoNaLa](https://arxiv.org/pdf/1805.08949.pdf)                                                                  | 2,379      | 500     | 2  | Program Synthesis  | Lexical    | Local   | Stackoverflow: QA        |
| [CONCODE](https://arxiv.org/abs/1808.09588v1)                                                                 | 100,000    | 2,000   | 1  | Program Synthesis  | Lexical    | Modular | Github                   |
| [Android](https://aclanthology.org/P18-1221/)                                                                 | 26,600     | 3,546   | 1  | Program Synthesis  | Lexical    | Local   | Map oriented, GitHub     |
| [CodeSearchNet](https://arxiv.org/abs/1909.09436)                                                           | 6,452,446  | 99      | 6  | Plain Text, Retrieval  | NDCG       | Modular | Github                   |
| [JuICe](https://arxiv.org/abs/1910.02216)                                                                   | 1,518,049  | 1,981   | 1  | Notebook Cell Gen. | Lexical    | Local   | Prog. assignment         |
| [TransCoder](https://arxiv.org/abs/2006.03511)                                                              | 721MB      | 1,410   | 3  | Program Translation | Lexical    | Modular | Github                   |
| [HumanEval](https://arxiv.org/abs/2107.03374)                                                               | -          | 164     | 1  | Program Synthesis  | Execution  | Modular | Interview Question       |
| [HumanEval-X](https://arxiv.org/abs/2303.17568)                                                             | -          | 820     | 9  | Synthesis & Translation  | Execution  | Modular | Interview Question       |
| [MBPP](https://arxiv.org/abs/2108.07732)                                                                    | -          | 974     | 1  | Program Synthesis  | Execution  | Modular | Interview Question       |
| [CodeXGLUE](https://arxiv.org/abs/2102.04664)                                                               | 2,840,000  | 759,000 | 9  | 10 Tasks           | Lexical    | Local   | N/A                      |
| [AVATAR](https://arxiv.org/abs/2108.11590)                                                                  | 5,937      | 1,693   | 2  | Program Translation | Lexical    | Global  | Problem Solving          |
| [TFix](http://proceedings.mlr.press/v139/berabi21a.html)                                                                    | 84,846     | 10,504  | 1  | Program Repair     | Lexical    | Local   | Github                   |
| [CCSD](https://openreview.net/forum?id=zv-typ1gPxA)                                                                    | 84,316     | 6,533   | 1  | Program Summarization  | Lexical    | Modular | Linux Kernel             |
| [TL-CodeSum](https://www.ijcai.org/proceedings/2018/314)                                                              | 55,766     | 6,971   | 1  | Program Summarization  | Lexical    | Modular | Github                   |
| [CodeNet](https://arxiv.org/abs/2105.12655)                                                                 | 8,906,769  | 2,783,365 | 55 | Classification, similarity | Lexical    | Global  | Problem Solving          |
| [TransCoder-ST](https://arxiv.org/abs/2110.06773)                                                           | 333,542    | 103,488 | 3  | Program Translation | Execution  | Modular | Github                   |
| [DSP](https://arxiv.org/abs/2201.12901)                                                                     | -          | 1,119   | 1  | Notebook Cell Gen. | Execution  | Local   | Math and Data Science    |
| [MTPB](https://openreview.net/forum?id=iaYcJKpY2B_)                                                                    | -          | 115     | 1  | Multi-turn Code Gen. | Execution  | Local   | Problem Solving          |
| [Exe-DS](https://arxiv.org/abs/2211.09374)                                                                  | 119,266    | 534     | 1  | Notebook Cell Gen. | Execution  | Local   | Data Science             |
| [DS-1000](https://arxiv.org/abs/2211.11501)                                                                 | -          | 1,000   | 1  | Notebook Cell Gen. | Execution  | Local   | Data Science             |
| [MoCoNaLa](https://arxiv.org/pdf/2203.08388.pdf)                                                                | -          | 896     | 1  | Program Synthesis  | Lexical    | Local   | StackOverflow            |
| [ARCADE](https://arxiv.org/abs/2212.09248)                                                                  | -          | 1,082   | 1  | Notebook Cell Gen. | Lexical    | Local   | Data Science             |
| [ODEX](https://arxiv.org/abs/2212.10481)                                                                    | -          | 945     | 1  | Program Synthesis  | Execution  | Local   | StackOverflow            |
| [MBXP](https://arxiv.org/abs/2210.14868)                                                                    | -          | 13,877  | 10 | Program Synthesis  | Execution  | Modular | Interview Question       |
| [XLCoST](https://arxiv.org/abs/2206.08474)                                                                  | 496,333    | 45,394  | 7  | 10 Task            | Lexical    | Local, Global | GitHub          |
| [DeepFix](https://www.iisc-seal.net/publications/aaai17.pdf)                                                                 | 37,000     | 7,000   | 1  | Program Repair     | Ececution  | Global  | Compile Error, Students  |
| [Defects4J](https://people.cs.umass.edu/~rjust/publ/defects4j_issta_2014.pdf)                                                               | -          | 835     | 1  | Program Repair     | Execution  | Local, Global | N/A                  |
| [APPS](https://github.com/hendrycks/apps)                                                                    | 5,000      | 5,000   | 1  | Program Synthesis  | Execution  | Global  | Interview Question       |
| [CodeContests](https://www.science.org/stoken/author-tokens/ST-905/full)                                                            | 4,432,447  | 32,181  | 3  | Program Synthesis  | Execution  | Global  | Problem Solving          |
| [CoderEval](https://arxiv.org/abs/2302.00288)                                                               | -          | 460     | 2  | Program Synthesis  | Execution  | Modular, Global | GitHub |
| [xCodeEval](https://arxiv.org/abs/2303.03004)                                                | 19,915,150 | 159,464 | 17 | 7 Tasks            | Execution  | Global  | Problem Solving          |



### What to Evaluate?

It's an easy question, but hard to answer. The way most of the research group and Ph.D. student evaluate LLM is, `How can I create more evaluation tables with minimal effort`. This is because immense publication pressure as well as the `Fear of missing out`. Let's see an example. Now in the western culture, "pronoun" or how someone identify himself is a big social movement that's being also included in the law. But none of the language model evaluation now a days evaluate `Named Entity Recognition` (NER) or `Parts of Speech tagging` (POS) since it's evaluation is a bit complicated and sometimes requires domain extertise on interpreting results. However it is inherintly important to evaluate LLMs understanding of NER or POS tagging. Also may be `NER` or `POS` tagging is not flashy enough to tweet (!!!).

So as a researcher, it is important to stating two important aspect,

1. What I'm evaluating.
2. What's missing in the evaluation.

Decades of benchmark creation effort certainly has a value embedded rather than finding cherry picked flashy LLM fails. The above table summarizes a good NLP evaluation benchmarks. However it fails miserably on many different aspects like, 

1. Evaluation on many Specific Social Science aspects.
2. Evaluation on Political biases.
3. Evaluation on Harmfullness and Helpfulness. 

There's been amazing continious effort of making LLM **less** Harmfull and **effectively** helpful at Anthropic. I would recommend few article on this if you have more interest on these topics.

It's been written in Open AI System card that their LLMs are evaluted on 50 Red teamming team(s) or individial experts on the certain fields. It's a shame that it's not even mentioned that what are the red teaming topics that they considered. This trend of not sharing the details due to citing industry competitiveness will surely continue until opensource cathces up on Red Teaming. I see a lot of Opensource community is driving LLM research like EleutherAI, BigScience, Aya. It would be great to have them picking up the Red Teaming effort. I cannot see a world where red teaming is unsuccessfull within opensource community. 

That being said, I'll conclude this section by inviting researchers to always summarize their evaluation outcome and adding limitations. When a new LLM comes in wilderness, in the paper (or now a days so called technical report prepared for VC funding), there should be a summary of evaluation outcome, `Why a set of evaluation benchmarks/protocols are selected to evaluate what downstream capability?`. 

<!-- extrinsic vs intirinsic evaluation -->

arrangement 
citation
collaspe

whats wrong with eval datasets
importance of time
training mmetadata of time
twitter agent


