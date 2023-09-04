+++
title = "xCodeEval: A Large Scale Multilingual Multitask Benchmark for Code Understanding, Generation, Translation and Retrieval"
date = 2023-03-06T00:00:00

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Mohammad Abdullah Matin Khan", "M Saiful Bari", "Xuan Long Do", "Weishi Wang", "Md Rizwan Parvez", "Shafiq Joty"]

# Publication type.
# Legend:
# 0 = Uncategorized
# 1 = Conference paper
# 2 = Journal article
# 3 = Manuscript
# 4 = Report
# 5 = Book
# 6 = Book section
publication_types = ["1"]

# Publication name and optional abbreviated version.
publication = "Arxiv"
publication_short = "Arxiv-preprint"

# Abstract.
abstract = "AI systems that can create codes as solutions to problems or assist developers in writing codes can increase productivity and make programming more accessible. Recently, pre-trained large language models have shown impressive abilities in generating codes from natural language descriptions, repairing buggy codes, translating codes between languages, and retrieving relevant code segments. However, the evaluation of these models has often been performed in a scattered way on only one or two specific tasks, in a few languages, at a partial granularity (e.g., function) level, and in many cases without proper training data. Even more concerning is that in most cases the evaluation of generated codes has been done in terms of mere lexical overlap with a reference code rather than actual execution. We introduce xCodeEval, the largest executable multilingual multitask benchmark to date consisting of 25M document-level coding examples (16.5B tokens) from about 7.5K unique problems covering up to 11 programming languages with execution-level parallelism. It features a total of seven tasks involving code understanding, generation, translation and retrieval. xCodeEval adopts an execution-based evaluation and offers a multilingual code execution engine, ExecEval that supports unit test based execution in all the 11 languages. To address the challenge of balancing the distributions of text-code samples over multiple attributes in validation/test sets, we further propose a novel data splitting and a data selection schema based on the geometric mean and graph-theoretic principle. Experimental results on all the tasks and languages show xCodeEval is a promising yet challenging benchmark as per the current advancements in language models."

# Summary. An optional shortened abstract.
summary = "We introduce xCodeEval, the largest executable multilingual multitask benchmark to date consisting of 25M document-level coding examples from about 7.5 K unique problems covering up to 17 programming languages with execution-level parallelism."

# Digital Object Identifier (DOI)
doi = ""

# Is this a featured publication? (true/false)
featured = true

# Tags (optional).
#   Set `tags = []` for no tags, or use the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["deep-learning", "multi-lingual", "language-model", "programming-language"]

# Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references 
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects = []

# Links (optional).
url_pdf = ""


# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# links = [{name = "Website", url = "https://www.taylorfrancis.com/books/9780429820915"}]
links = [{name = "Paper", url = "https://arxiv.org/abs/2303.03004"}, {name = "Code", url = "https://github.com/ntunlp/xCodeEval"}, {name="huggingface", url="https://huggingface.co/datasets/NTU-NLP-sg/xCodeEval"}]

# Does this page contain LaTeX math? (true/false)
math = true

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  caption = "Image credit: [**Augvic**]()"

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Center"
+++
