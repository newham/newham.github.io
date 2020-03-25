---
layout : post
title : latex ieee模板中文版
date : 2020-03-25 17:38:33 +0800
categories : latex
description : 让latex ieee支持中文
---

1.添加：

% *** 中文支持-start ***

\usepackage{cite}

\usepackage{amsmath,amssymb,amsfonts}

\usepackage{algorithmic}

\usepackage{graphicx}

\usepackage{float} 

\usepackage{subfigure}

\usepackage{textcomp}

\usepackage{xcolor}

\usepackage{ctex}

\usepackage{booktabs}

\usepackage{caption}

\usepackage[colorlinks]{hyperref}

% *** 中文支持-end ***



2.文件头添加【用texstudio】

%!TEX program = xelatex 



3.配置文件【用vscode】

{

​    "latex-workshop.latex.recipes": [

​      {

​        "name": "xelatex",

​        "tools": [

​          "xelatex",

​          "bibtex",

​          "xelatex",

​          "xelatex"

​        ]

​      }

​    ],

​    "latex-workshop.latex.tools": [

​      {

​        "name": "latexmk",

​        "command": "latexmk",

​        "args": [

​          "-synctex=1",

​          "-interaction=nonstopmode",

​          "-file-line-error",

​          "-pdf",

​          "%DOCFILE%"

​        ]

​      },

​      {

​        "name": "xelatex",

​        "command": "xelatex",

​        "args": [

​          "-synctex=1",

​          "-interaction=nonstopmode",

​          "-file-line-error",

​          "%DOCFILE%"

​        ]

​      },

​      {

​        "name": "bibtex",

​        "command": "bibtex",

​        "args": [

​          "%DOCFILE%"

​        ]

​      }

​    ],

​    "latex-preview.command": "xelatex"

  }