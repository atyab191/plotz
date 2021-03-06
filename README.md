# PlotZ

If you are plotting graphs for scientific publication, chances are that

- your data has been produced by a python program (or by some other
  C/C++/Fortran code, but you want to post-process it in a higher-level language
  like python);
  
- you are eventually going to write a paper using LaTeX in which you'll want
  your figures to be nice and tightly integrated with the rest of the document;
  
- you'll then reuse the same figures in a Beamer presentation, where you will
  still want everything to be nicely integrated with your theme... but you might
  not like having to re-work everything so that fonts are legible and lines
  thick enough.

`PlotZ` aimz at producing publication-quality plots for inclusion in LaTeX
documents. It is designed to be as simple to use as possible, with a Python API
allowing to produce, post-process and plot your data in the same
environment. PlotZ actually produces TikZ code, that will seamlessly integrate
in your LaTeX documents/presentations. The provided command allows resizing
PlotZ images on the fly, so that your picture will always come right, whether it
appears as a small subfigure in a paper or in a Beamer slide.

## Examples gallery

[<img src="examples/gallery.svg?raw=true&sanitize=true" alt="Gallery" />](examples)

Look at the [Examples Gallery](examples) to see what `PlotZ` can produce (and
how to do it).

## Installation

Simply clone this repository somewhere, and source the accompanying environment
file to setup the relevant environment variables:

```sh
git clone https://github.com/ffevotte/plotz.git
source plotz/env.sh
```


## Basic usage

### Python script

<img src="examples/00-base/00-gettingStarted/plot.svg?raw=true&sanitize=true"
     alt="Example plot" />

Put the following content in a python file (named `myplot.py`, for example):

```python
from plotz import *
from math import sin, pi

with Plot("myfigure") as p:
    p.title = r"My first \texttt{PlotZ} plot"
    p.x.label = "$x$"
    p.y.label = "$y$"
    p.y.label_rotate = True

    p.plot(Function(sin, samples=50, range=(0, pi)),
           title=r"$\sin(x)$")

    p.legend("north east")
```

then execute the code:

```sh
source /path/to/plotz/env.sh
python myplot.py
```

You should get two files:

- `myfigure.pdf` is a rendered version of your figure (similar to the image
  shown above),
- `myfigure.tex` is a LaTeX file that you can import in a LaTeX document


### LaTeX document

In order to include a `PlotZ` figure in a LaTeX document, the only steps needed
are:

- include the `plotz` package in your preamble
- use the `plotz` command to include your figure

For example:

```latex
\documentclass{article}
\usepackage{plotz}

\begin{document}

\begin{figure}[ht]
  \centering
  \plotz[width=0.8\textwidth]{myfigure}
  \caption{A \texttt{PlotZ} figure}
\end{figure}

\end{document}
```


If you specify an optional size to the `plotz` command, the plot will then be
scaled automatically to obtain a figure of the desired size. Notice how this
differs from a simple scaling (such as what would be obtained using
`\resizebox{\textwidth}{!}{...}` or `\includegraphics[width=\textwidth]{...}`)
in that lines thicknesses, font sizes, *etc.* remain constant.

<img src="examples/00-base/00-gettingStarted/document.svg" />

The same figure can also be used in a Beamer presentation, where it will adapt
to its new environment. Notice how the font changed to be consistent with the
beamer theme. And also note that font size and line thickness remain big enough
for the figure to remain legible even by the audience sitting in the back of the
room:

<img src="examples/00-base/00-gettingStarted/presentation.svg"
    style="border: 1px solid blue"/>

<p style="margin-top: 5em"></p>

## Contributing

If you make improvements to this code or have suggestions, please do not
hesitate to fork the repository or submit bug reports
on [github](https://github.com/ffevotte/plotz.git). The repository's URL is:

    https://github.com/ffevotte/plotz.git


## License

Copyright (C) 2017 François Févotte.

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program. If not, see [http://www.gnu.org/licenses/]().

### Acknowledgement

The color schemes included in `PlotZ` come from the
excellent [ColorBrewer](http://colorbrewer2.org/) tool.
