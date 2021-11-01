+++
title = "Multitask Prompted Training Enables Zero-Shot Task Generalization"
date = 2021-10-15T00:00:00

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Victor Sanh", "Albert Webson", "Colin Raffel", "Stephen H. Bach", "Lintang Sutawika", "Zaid Alyafeai", "Antoine Chaffin", "Arnaud Stiegler", "Teven Le Scao", "Arun Raja", "Manan Dey", "M Saiful Bari", "Canwen Xu", "Urmish Thakker", "Shanya Sharma Sharma", "Eliza Szczechla", "Taewoon Kim", "Gunjan Chhablani", "Nihal Nayak", "Debajyoti Datta", "Jonathan Chang", "Mike Tian-Jian Jiang", "Han Wang", "Matteo Manica", "Sheng Shen", "Zheng Xin Yong", "Harshit Pandey", "Rachel Bawden", "Thomas Wang", "Trishala Neeraj", "Jos Rozen", "Abheesht Sharma", "Andrea Santilli", "Thibault Fevry", "Jason Alan Fries", "Ryan Teehan", "Stella Biderman", "Leo Gao", "Tali Bers", "Thomas Wolf", "Alexander M. Rush"]

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
publication = "Arxiv-preprint"
publication_short = "Arxiv"

# Abstract.
abstract = "Large language models have recently been shown to attain reasonable zero-shot generalization on a diverse set of tasks. It has been hypothesized that this is a consequence of implicit multitask learning in language model training. Can zero-shot generalization instead be directly induced by explicit multitask learning? To test this question at scale, we develop a system for easily mapping general natural language tasks into a human-readable prompted form. We convert a large set of supervised datasets, each with multiple prompts using varying natural language. These prompted datasets allow for benchmarking the ability of a model to perform completely unseen tasks specified in natural language. We fine-tune a pretrained encoder-decoder model on this multitask mixture covering a wide variety of tasks. The model attains strong zero-shot performance on several standard datasets, often outperforming models 16x its size. Further, our approach attains strong performance on a subset of tasks from the BIG-Bench benchmark, outperforming models 6x its size. All prompts and trained models are available."

# Summary. An optional shortened abstract.
summary = "T0 shows zero-shot task generalization on English natural language prompts, outperforming GPT-3 on many tasks, while being 16x smaller!"

# Digital Object Identifier (DOI)
doi = ""

# Is this a featured publication? (true/false)
featured = true

# Tags (optional).
#   Set `tags = []` for no tags, or use the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["deep-learning", "language-model"]

# Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references 
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects = []

# Links (optional).
url_pdf = "https://arxiv.org/abs/2110.08207"


# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# links = [{name = "Website", url = "https://www.taylorfrancis.com/books/9780429820915"}]
links = [{name = "Paper", url = "https://arxiv.org/abs/2110.08207"}]

# Does this page contain LaTeX math? (true/false)
math = true

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  caption = "Image credit: [**T0**]()"

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Center"
+++
