---
title: 'Using Emacs as LaTeX editor'
date: 9999-12-31
permalink: /posts/todo/emacs-latex/
tags:
  - emacs
  - editor
  - latex
---

# Using Emacs as LaTeX editor
The following guide focuses on Debian-based Linux systems.

## Software setup

### Install Emacs
Different options, I prefer the terminal-only version. 
```console
sudo apt install emacs-nox
```

### Install TexLive plus some extras

```console
sudo apt install texlive texlive-lang-german texlive-latex-extra texlive-science
```

```console
Alternatively, for full funtionality (will need much more disk space):
sudo apt install texlive texlive-full
```


### Install AUCTeX
[AUCTeX](https://www.gnu.org/software/auctex/) is an extensible package for writing and formatting TeX files in GNU Emacs.
```console
sudo apt install auctex
```


## Update Emacs configuration

```lisp
(load "auctex.el" nil t t)
(load "preview-latex.el" nil t t)
```

Adding the following line to your `.emacs` configuration file will make Emacs compile tex files to PDF files by default.
```lisp
(setq latex-run-command "pdflatex")
```

## Compile to PDF

In Emacs, use `C-c C-a` to launch the compilation to PDF. In case there are no errors, the PDF file should be safed to the directory where the tex file is stored and be opened in your PDF viewer.
