+++
title = "What Language Model to Train if You Have One Million GPU Hours?"
date = 2022-03-01T00:00:00

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Teven Le Scao", "Thomas Wang", "Daniel Hesslow", "Lucile Saulnier", "Stas Bekman", "M Saiful Bari", "Stella Biderman", "Hady Elsahar", "Jason Phang", "Ofir Press", "Colin Raffel", "Victor Sanh", "Sheng Shen", "Lintang Sutawika", "Jaesung Tae", "Zheng Xin Yong", "Julien Launay", "Iz Beltagy"]

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
publication = "Challenges & Perspectives in Creating Large Language Models"
publication_short = "In **ACL-2022** Workshop"

# Abstract.
abstract = "The crystallization of modeling methods around the Transformer architecture has been a boon for practitioners. Simple, well-motivated architectural variations that transfer across tasks and scale, increasing the impact of modeling research. However, with the emergence of state-of-the-art 100B+ parameters models, large language models are increasingly expensive to accurately design and train. Notably, it can be difficult to evaluate how modeling decisions may impact emergent capabilities, given that these capabilities arise mainly from sheer scale.Targeting a multilingual language model in the 100B+ parameters scale, our goal is to identify an architecture and training setup that makes the best use of our 1,000,000 A100-GPU-hours budget. Specifically, we perform an ablation study comparing different modeling practices and their impact on zero-shot generalization. We perform all our experiments on 1.3B models, providing a compromise between compute costs and the likelihood that our conclusions will hold for the target 100B+ model. In addition, we study the impact of various popular pretraining corpora on zero-shot generalization. We also study the performance of a multilingual model and how it compares to the English-only one. Finally, we consider the scaling behaviour of Transformers to chose the target model size, shape, and training setup."

# Summary. An optional shortened abstract.
summary = ""

# Digital Object Identifier (DOI)
doi = ""

# Is this a featured publication? (true/false)
featured = true

# Tags (optional).
#   Set `tags = []` for no tags, or use the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["deep-learning", "multi-lingual", "language-model"]

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
links = [{name = "Paper", url = "https://openreview.net/pdf?id=rI7BL3fHIZq"}]

# Does this page contain LaTeX math? (true/false)
math = true

# Featured image
[image]
  # Caption (optional)
  caption = "Image credit: [**Paper**](https://openreview.net/pdf?id=rI7BL3fHIZq)"

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Center"
+++
