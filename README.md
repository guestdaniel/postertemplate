Summary
=======

This repo contains a number of files which will help users create posters using LaTeX and KnitR. 

With questions, please contact Daniel Guest at guest121@umn.edu.

Files
=====

``bibliography.bib`` &mdash; sample bibliography written in biblatex style   
``beamerposter.sty`` &mdash; beamerposter package 
``beamerthemeconfposter.sty`` &mdash; theme for beamerposter, contains most color and block definitions   
``blank.Rnw`` &mdash; source file for blank poster (i.e., has no example content)   
``blank.tex`` &mdash; intermediary ``.tex`` file between ``.Rnw`` source and ``.pdf`` output for blank poster   
``blank.pdf`` &mdash; output document for blank poster   
``poster.Rnw`` &mdash; source file for example poster   
``poster.tex`` &mdash; intermediary ``.tex`` file between ``.Rnw source`` and ``.pdf`` output for example poster   
``poster.pdf`` &mdash; output document for example poster   

How To Use It
=============

*Compilation*

The poster is written in a combination of LaTeX and R code, with the source file ``poster.Rnw``. Changes to this file must first be knitted into a ``.tex`` file by KnitR. Then, the resulting ``.tex`` file must then be compiled into a ``.pdf`` file (or another output file of your choosing). Below, I've provided an example of how to perform this compilation manually in Bash. R Studio has features to perform these steps automatically! 

```bash
cd /where/the/poster/dir/is
Rscript -e "library(knitr); knitr('./poster.Rnw')"
latexmk -pdf poster.tex
```

*Change the colors and logo*

As is quite obvious, the example poster is styled to match the University of Minnesota's color scheme, but this is easy to change via the following steps:
1. A variety of colors are already defined in ``beamerthemeconfposter.sty``. Open ``beamerthemeconfposter.sty`` in a text editor and find "UNIVERSITY OF MINNESOTA COLORS".
2. Add new definitions of your own colors in the same format, or find existing color definitions which suit you. 
3. Replace every instance of UMNMaroon in ``poster.Rnw`` with your new colors as you see fit. In most places that use color names, it should be clear what the color is being used for. Changes made in ``poster.Rnw`` overwrite defaults in ``beamerthemeconfposter.sty``. 
4. Add your own logo into the poster directory, and replace "umnlogotemp" with the name of your logo file in ``beamerthemeconfposter.sty``

*Change the poster size*

To change the poster's size, simply change the sizes specified in ``poster.Rnw``:
1. The line ``\setlength{\paperwidth}{48in}`` controls the paper width
2. The line ``\setlength{\paperheight}{36in}`` controls the paper height

You can specify sizes in other units as well (such as cm or pt). 

*Change the columns*

The structure provided in ``poster.Rnw`` and ``blank.Rnw`` divides the poster into three columns: two smaller flanking columns and one larger middle column. However, it's easy to modify this to suit your needs (and even to divide individual columns into subcolumns). 

The poster content is enclosed in a ``frame`` environment, delimited by ``\begin{frame}`` and ``\end{frame}``. 
