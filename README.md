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

The poster is written in a combination of LaTeX and R code, with the source file ``poster.Rnw``. Changes to this file must first be knitted into a ``.tex`` file by KnitR. Then, the resulting ``.tex`` file must be compiled into a ``.pdf`` file (or another output file of your choosing). Below, I've provided an example of how to perform this compilation manually in Bash. R Studio has features to perform these steps automatically!

```bash
cd /where/the/poster/dir/is
Rscript -e "library(knitr); knitr('./poster.Rnw')"
latexmk -pdf poster.tex
```

As is quite obvious, the example poster is styled to match the University of Minnesota's color scheme, but this is easy to change via the following steps:
1. Open ``beamerthemeconfposter.sty`` in a text editor and find "UNIVERSITY OF MINNESOTA COLORS".
2. Replace the colors with your own choices, or add new definitions of your own colors.
3. Replace every instance of UMNMaroon in ``beamerthemeconfposter.sty`` and ``poster.Rnw`` with your new colors as you see fit. In most places that use color names, it should be clear what the color is being used for.
4. Add your own logo into the poster directory, and replace "umnlogotemp" with the name of your logo file in ``beamerthemeconfposter.sty``
