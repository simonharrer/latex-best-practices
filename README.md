# LaTeX Best Practices

## At the very beginning

```latex
\RequirePackage[l2tabu, orthodox]{nag} % detect deprecated use of latex packages and commands
```

## During writing

```latex
\usepackage[notref,notcite]{showkeys} % useful when writing the paper
```
## Commands to find issues faster

```latex
\overfullrule=2cm % allows to find overfull hboxes much quicker
```

## figures only appear after their first use, never ever before   

```latex
\usepackage{flafter} 
```

## Inspirational Quotes

```latex
% import
\usepackage{epigraph}

% use
\chapter{Background}
% optionally, use \epigraphhead[30]{\epigraph...} to put the epigraph above the chapter name
\epigraph{If I have seen further, it is by standing on the shoulders of giants.}{\emph{Isaac Newton}}
```

## Custom Counters and References

```latex
% commands
\newcounter{requirement}% create counter <requirement> with <0> as initial value
\renewcommand*\therequirement{R\arabic{requirement}}% ensure that the counter is always printed as R<requirement>
\newcommand{\requirement}{%
(%
\refstepcounter{requirement}% <requirement> = <requirement> + <1>
\therequirement% print R<requirement>
)%
}

% usage
\requirement\label{req:fast-tests} % (R1)
\requirement\label{req:make-world-a-better-place} % (R2)

\ref{req:fast-tests} % R1
\ref{req:make-world-a-better-place} % R2
```

I could have created the label as part of the macro, but then, most LaTeX editors will not be able to code complete these labels as they cannot determine that any passed parameters are labels. Moreover, [textools](https://github.com/simonharrer/textools) can detect these labels and check whether they are unused.

## Tables

```latex
% import
\usepackage{booktabs}

% use
\begin{tabular}{rl}
	\toprule
	\textbf{name} & \textbf{version} \\ 
	\midrule
	tool A & 1.0\\
	tool B & 5.3\\
	tool C & 4.0\\
	\bottomrule
\end{tabular}
```

## Packages which simply help always

```latex
\usepackage{warning} % for warning messages
\usepackage{refcheck} % show unused labels
\usepackage{strict} % check for not using undefined environments

\usepackage{microtype} % nicer output
\usepackage{hfoldsty} % nicer output
\usepackage{lmodern} % use the modern fonts
\usepackage{charter} % use the charter font

\usepackage[ngerman,USenglish]{babel} % language selection
\usepackage[T1]{fontenc} % western languages encoding
\usepackage[utf8]{inputenc} % set encoding to UTF-8
```

## TODOs

```latex
% import
\usepackage{todonotes}

% usage
\todo{TODO as a margin block}
\todo[inline]{TODO within the text}
\missingfigure{Description of missing figure}

\listoftodos
```

## URLs and references

```latex
\usepackage[hyphens]{url} % detection of urls
\usepackage{hyperref} % should be imported after all other packages as it changes a lot
\usepackage[all]{hypcap} % Adjusting the anchors of captions
\usepackage[hyperpageref]{backref} % add backlinks from the references to the cited pages
\usepackage[capitalise,nameinlink]{cleveref} % always prepend the correct type before each reference
```

## Quotations

```latex
\usepackage[strict=true,english=american]{csquotes}
```

## Acroynms

```latex
% import
\usepackage[printonlyused,withpage]{acronym}

% usage list
\begin{acronym}
  \acro{API}{Application Programming Interface}
\end{acronym}

% usage in text
\ac{API} % API, show full if first use
\acf{API} % always Application Programming Interface (API)
\acp{API} % APIs, show full if first use
\acfp{API} % always Application Programming Interfaces (APIs)
\acs{API} % always API
```
## Keywords besides paragraph

```latex
% import
\usepackage{marginnote} % notes on the margin of the page

% ensures this is always correctly aligned
% see http://tex.stackexchange.com/questions/16141/align-marginpar-with-beginning-of-paragraph
\let\brokenmarginnote\marginnote
\renewcommand{\marginnote}[1]{\hspace{0pt}\brokenmarginnote{#1}}

% use footnotesize as a font size to push the margin notes into the background
\renewcommand{\marginnote}[1]{\hspace{0pt}\brokenmarginnote{{\footnotesize #1}}}

% usage
\marginnote{This is put right next to the paragraph}
```

## Special Commands

```latex
% user stories
\newcommand{\userstory}[3]{\textbf{As a} #1, \textbf{I want to} #2 \textbf{so that I can} #3.}

% describing XML elements, attributes, and values of attributes
\newcommand{\xml}[1]{\texttt{<#1>}} % <element> in typewriter
\newcommand{\attr}[1]{\texttt{@#1}} % @attribute in typewriter
\newcommand{\attrval}[2]{\texttt{#1}=\val{#2}} % attribute="value" in typewriter (only equals sign is normal)
\newcommand{\val}[1]{\texttt{"#1"}} % "value" in typewriter
```



## Space Saving Techniques

### Use Times Instead

```tex
\usepackage{mathptmx}
```

### Smaller Font Size for References

```tex
{\footnotesize
\bibliography{bibfile}}
```

### Remove Space Between Bibliography Entries

```tex
% saves almost half a page by removing space between references
\let\oldbibliography\thebibliography \renewcommand{\thebibliography}[1]{%
   \oldbibliography{#1}%
   \setlength{\itemsep}{0pt}%
}
```

### Shorten a paragraph

```tex
% import
\usepackage{microtype}
\SetExpansion
[ context = sloppy,
stretch = 30,
shrink = 36,
step = 1 ]
{ encoding = {OT1,T1,TS1} }
{ }
%source: http://tex.stackexchange.com/a/280936/9075

% use
{\microtypecontext{expansion=sloppy}
This text shrinks a bit more to help saving a line if only one word is put in the last line of the paragraph.
}

```
