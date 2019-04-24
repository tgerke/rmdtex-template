# rmdtex-template

I often need to write short reports which are not full blown manuscripts, e.g. annual grant progress reports. Though such documents don't need to adhere to a strict template, I still want them to look nice. I've accomplished this for years by writing directly in LaTeX, but I want to align my process with my recent transition to composing most docs in RStudio/Rmd. Ultimately though, I don't want to abandon the LaTeX look in the compiled document. Thankfully, RStudio will render a LaTeX pdf, but formatting beyond the defaults (which are still nice!) can be a bit mysterious. This repository holds my working template for such purposes.

Here's a minimal example of what the defaults within a `.Rmd` will give you:

```
---
title: "A short report"
author: "Travis Gerke"
date: "`r format(Sys.time(), '%Y %B %d')`"
output: 
   pdf_document: 
      keep_tex: yes
latex_engine: pdflatex
---
   
# Introduction

`r paste(stringi::stri_rand_lipsum(2), collapse = "\n\n")`

# Progress

`r paste(stringi::stri_rand_lipsum(2, start_lipsum = FALSE), collapse = "\n\n")`

# Future Directions

`r paste(stringi::stri_rand_lipsum(3, start_lipsum = FALSE), collapse = "\n\n")`
```
![Default rendered pdf](figures/default.png)

Now, two specific things I'd like to change are: 

* Left-justify the title/author/date section
* Modify the font specs used in section titles

A solution to these two problems easily generalizes to the broader question of "How do I format the title and H1-H6 specs in the context of LaTeX rendering from `.Rmd` files?"

---

To start, we need to identify what LaTeX template R Markdown is currently using (h/t [SO](https://stackoverflow.com/questions/52706006/accessing-yaml-parameters-as-macros-within-external-latex-files/52779863#52779863)). The relevant remote repo is [here](https://github.com/rstudio/rmarkdown/tree/master/inst/rmd/latex), and you can copy the local version you're using into your working directory with this line: 

```
file.copy(system.file("rmd/latex/default-1.17.0.2.tex",
          package = "rmarkdown"), "template.tex")
```