Summary
=======

This repository contains a set of files to help users create posters for psychology conferences using LaTeX and knitr. LaTeX and knitr are a powerful combination. Together, they allow the creation of posters which are elegant, replicable, and easy to edit and adapt. Moreover, all of the tools involved are open source and free. 

A huge thank you to the creators of beamerposter, to Nathaniel Johnson, and to the Computational Physics and Biophysics Group at Jacobs University. Much of the material in this repository is sourced directly from them with only small modifications.

With questions, please contact Daniel Guest at guest121@umn.edu.

Introduction
============

This poster template assumes some familiarity with LaTeX, R, and knitr. If you're not sure what some of these things are, the links below provide some great tutorials and resources to learn more about them. 

*LaTeX*
- [Getting Started with LaTeX](https://www.maths.tcd.ie/~dwilkins/LaTeXPrimer/)
- [Getting started with TeX, LaTeX, and friends](https://www.tug.org/begin.html)

*R*
- [Getting started with R](https://support.rstudio.com/hc/en-us/articles/201141096-Getting-Started-with-R)
- [R: Getting started with R](http://scs.math.yorku.ca/index.php/R:_Getting_started_with_R)

*knitr*
- [knitr](https://yihui.name/knitr/)
- [A Beginner's Tutorial for knitr](https://joshldavis.com/2014/04/12/beginners-tutorial-for-knitr/)

Requirements
============

- LaTeX, with a number of common packages installed (see ``.Rnw`` file preambles)
- R, with ggplot2, cowplot, and knitr installed 
- biber, if you want bibliography support 

Files
=====

``bibliography.bib`` &mdash; sample bibliography written in biblatex style   
``beamerposter.sty`` &mdash; beamerposter package   
``beamerthemeconfposter.sty`` &mdash; theme for beamerposter, contains most color and block definitions   
``blank.Rnw`` &mdash; source file for blank poster (i.e., has no example content)   
``blank.tex`` &mdash; intermediary ``.tex`` file between ``.Rnw`` source and ``.pdf`` output for blank poster   
``blank.pdf`` &mdash; output document for blank poster   
``poster.Rnw`` &mdash; source file for example poster   
``poster.tex`` &mdash; intermediary ``.tex`` file between ``.Rnw`` source and ``.pdf`` output for example poster   
``poster.pdf`` &mdash; output document for example poster   

How To Use It
=============

*Compilation*

The poster is written in a combination of LaTeX and R code in the source file ``poster.Rnw``. Changes to this file must first be knitted into a ``.tex`` file by knitr. Then, the resulting ``.tex`` file must then be compiled into a ``.pdf`` file (or another output file of your choosing). Below, I've provided an example of how to perform this compilation manually in Bash.

```bash
cd /where/the/poster/dir/is
Rscript -e "library(knitr); knitr('./poster.Rnw')"
latexmk -pdf poster.tex
```

RStudio can also can do all of this for you! Look [here](https://support.rstudio.com/hc/en-us/articles/200552056-Using-Sweave-and-knitr) and [here](https://yihui.name/knitr/demo/rstudio/) for more info about how to use RStudio with knitr. 

*Change the colors and logo*

As is quite obvious, the example poster is styled to match the University of Minnesota's color scheme, but this is easy to change:
1. A variety of colors are already defined in ``beamerthemeconfposter.sty``. Open ``beamerthemeconfposter.sty`` in a text editor and find "UNIVERSITY OF MINNESOTA COLORS".
2. Add new definitions of your own colors in the same format, or find existing color definitions which suit you. 
3. Replace every instance of UMNMaroon in ``poster.Rnw`` with your new colors as you see fit. In most places that use color names, it should be clear what the color is being used for. Changes made in ``poster.Rnw`` overwrite defaults in ``beamerthemeconfposter.sty``. 
4. Add your own logo into the poster directory, and replace "umnlogotemp" with the name of your logo file in ``beamerthemeconfposter.sty``

*Change the poster size*

To change the poster's size, you need to do two things. First, change the LaTeX lengths specified in ``poster.Rnw``:
1. The line ``\setlength{\paperwidth}{48in}`` controls the paper width
2. The line ``\setlength{\paperheight}{36in}`` controls the paper height

Second, change the ``\usepackage{beamerposter}`` call to include your new sizes (in cm). That is, ``\usepackage[scale=1.25]{beamerposter}`` should become ``\usepackage[size=custom, width=x, height=y, scale=1.25]{beamerposter}`` where x and y are your new sizes in cm.

You can specify sizes in other units as well (such as cm or pt). 

*Change the columns*

The structure provided in ``poster.Rnw`` and ``blank.Rnw`` divides the poster into three columns: two smaller flanking columns and one larger middle column. However, it's easy to modify this to suit your needs (and even to divide individual columns into subcolumns). 

The poster content is enclosed in a ``frame`` environment, delimited by ``\begin{frame}`` and ``\end{frame}``. Within the frame environment is a ``columns`` environment, similarly delimited. Inside the ``columns`` environment are multiple ``column`` environments, which are arranged on the poster as columns left to right in the order in which they are included in the ``.Rnw`` file. Each ``column`` has a particular width, which is passed as an argument to the column as such: 

```latex
\begin{column}{width}
% This column's content here, inside block environments!
\end{column}
```  

You can modify this width, but keep in mind that the paper has a finite size. If you make the columns too wide, they'll run off the page. If you make the columns too narrow, they won't take up the full page. So rather than use fixed sizes, we use sizes which are proportional to the ``\paperwidth``. Look in the ``.Rnw`` file for a comment block which begins with "Define the column width and poster size" to see how this works. 

First, choose how many columns you want. To be more specific, choose how many slices you want to divide the poster into. In the example ``poster.Rnw``, even though it has three columns of content, imagine that it has four divisions, because the second larger column is the size of two divisions, while the smaller flanking columns are the size of one division. Then, choose how much space you want between columns in terms of the paper's width. A reasonable value (the default) is ``0.024`` times ``\paperwidth``. However, you can choose to have more or less space between columns. Finally, modify the lengths defined below the comments according to the formulas in the comments. The values used in ``poster.Rnw`` are used an example in the comments, but another example is provided below:

Let's assume we want the poster divided into five segments, with one narrow column constituting one division on the left, and then two columns twice the width of the first column constituting two divisions each in the middle and on the right. Furthermore, let's assume we want an extra-thick space between the columns. Specifically, we'll choose ``0.035`` times ``\paperwidth`` as our separation between columns, and follow the instructions in ``poster.Rnw`` to arrive at:

```latex
\newlength{\sepwid}
\newlength{\onecolwid}
\newlength{\twocolwid}
\newlength{\threecolwid}
\setlength{\paperwidth}{48in} % Poster width
\setlength{\paperheight}{36in} % Poser height
\setlength{\sepwid}{0.035\paperwidth} % 0.035 paperwidth separation between columns
\setlength{\onecolwid}{0.158\paperwidth} % (1/5)*(1-(5+1)*0.035)
\setlength{\twocolwid}{0.351\paperwidth} % 2*0.158 + 0.035
\setlength{\threecolwid}{0.544\paperwidth} % 3*0.158 + 2*0.035
\setlength{\topmargin}{-0.5in}
```

Then, our columns environment would be specified as:

```latex
\begin{columns}
	\begin{column}{\sepwid} \end{column} % Empty spacer column
	\begin{column}{\onecolwid} % Smaller left column
	\end{column}
	\begin{column}{\sepwid} \end{column} % Empty spacer column
	\begin{column}{\twocolwid} % Bigger middle column
	\end{column}
	\begin{column}{\sepwid} \end{column} % Empty spacer column
	\begin{column}{\twocolwid} % Bigger right column
	\end{column}
	\begin{column}{\sepwid} \end{column} % Empty spacer column
\end{columns}
```
