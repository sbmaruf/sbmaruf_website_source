+++
# Project title.
title = "Malay-English Neural Machine Translation System."

# Date this page was created.
date = 2017-06-12T00:00:00

# Project summary to display on homepage.
summary = "This is a tool to translate an English sentence into Malay and vice versa."

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["Deep Learning"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references 
#   `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides = ""

# Links (optional).
url_pdf = ""
url_slides = ""
url_video = ""
url_code = ""

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
links = [{icon_pack = "fab", icon="twitter", name="Follow", url = "https://twitter.com/sbmaruf"}]

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder. 
[image]
  # Caption (optional)
  caption = ""
  
  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "TopLeft"
+++

This is a tool to translate an English sentence into Malay and vice versa. Developing a translation tool for low-resource languages like Malay has always been a challenge. The main challenge comes from the fact that machine translation systems typically rely on a huge amount of sentence-parallel data, and creating such datasets is an expensive process. In our work, we collected parallel datasets from various sources including News, OpenSubtitiles (OPUS), Ted talks, and Youtube video. Therefore, our corpus is quite generic and covers both texts and conversations.

We used various state of the art deep **Neural Machine Translation** (NMT) architecture for training our model. More specifically we use both **seq2seq** and **transformer-net** architecture for finding our best model. For pre-processing and post-processing datasets we used various tools of **moses**. To train our model we used **OpenNMT-py** framework which is very standard in the NMT community for it's robust and modular implementation.

Currently the live demo can only be accessed from inside NTU network.
<form action="http://172.21.145.63:4200">
    <input type="submit" value="The link of the demo" />
</form>