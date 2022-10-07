# Important note about bibliography handling

## For the impatient

Regarding bibliography files, you just have to edit the `Book/bibliofiles.tex`
file, stating (uncommenting) which files you need for the bibliography. No
changes are needed elsewhere.

The default bibliography processing backend is now `biber` (from September 2022
onwards). This implies that you have to tell your IDE that you are using `biber`
instead of `bibtex`. This applies to TeXStudio for example.


## More details

As of September 2022, nice work from Gonzalo Corral abandoned the `bibtex`
processing tool in favour of `biber`.

There a number of advantages and disadvantages on using `biber` (see for example
[here](https://tex.stackexchange.com/questions/25701/bibtex-vs-biber-and-biblatex-vs-natbib)
and [here](https://tex.stackexchange.com/questions/53247/why-is-biber-so-slow))
but the fact that it can use UTF-8 as the encoding for the bib files was the
number one reason for accepting this change.

The change in the backend processor caused a major headache as `biblatex`
requires specifying the bib files in the preamble, and we did not want to make
users deal with it. The solution we found was quick and dirty but it seems to
work: now the users just have to edit the `Book/bibliofiles` file to include the
required biblio files.


## If you still prefer (for whatever reason) `bibtex` as your backend

Gonzalo still kept some support for `bibtex` in the `Makefile` and `Book/book.tex` files. If you want to use the `bibtex` you have to:

- Define the ``\bibliosystem` variable in `Config/preamble.tex` to be equal to `bibtex``
- Convert the `biblio/biblio.bib` file to ISO-8859-1 encoding


# Important note about source code inclusion handling

To include source code listings you can edit the file `preamble.tex` and select
the backend to use commenting one of these two lines.
```
  \newcommand{\codesystem}{listings} % Valid options are listings or minted
  % \newcommand{\codesystem}{minted} % Valid options are listings or minted
```

The available options are
- listings: This is the option by default and the recommended one. It may have
  problems with long lines and with utf-8 characters.
- minted: This backend need the `pygments` python package, (it's included by
  default in overleaf). It can achieve better syntax coloring.

We refer you to the overleaf manual in both backends
[minted](https://es.overleaf.com/learn/latex/Code_Highlighting_with_minted) and
[listings](https://es.overleaf.com/learn/latex/Code_listing)

# Important note about glossary and symbols handling.

The glossaries package is used for the symbols and acronym list. The problem
here is twofold, the package requires the makeglossaries program, and it
doesn't work on overleaf by default (it only works if the main .tex document
is in the root folder, which is not the case).

To solve it we introduce an alternative backend, but it also has the problem
that the sorting is worse, and it doesn't work well with the presence of utf-8
characters in the acronyms.

This option is controlled by a toggle in `preamble.tex`, where `makeglossaries`
selects the default (and recommended) backend that uses an external program and
makenoidxglossaries selects the alternative backend for overleaf (and possibly
windows) 
```
  \newcommand{\glossariessystem}{makeglossaries} % Valid options are makeglossaries or makenoidxglossaries.
  % \newcommand{\glossariessystem}{makenoidxglossaries} % Valid options are makeglossaries or makenoidxglossaries.

```

We recommed that you only activate makenoidxglossaries if and only if you can't
use makeglossaries.
