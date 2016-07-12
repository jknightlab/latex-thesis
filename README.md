# Using LaTeX to write a thesis

Latex is a document preparation system that is useful for producing structured documents such as a thesis. It is particularly helpful when including many figures or tables.

### Installation

[TeXnicCenter](http://www.texniccenter.org/) is an editor which can be used to create, edit, compile and view latex files.

### Usage

When writing a long document such as a thesis, it is easier to use multiple separate files. This also allows certain chapters to be selected for each compilation.

#### File formats

Examples of the following files can be found in the  github repository

##### Main file

Create a folder which contains the main thesis.tex file, the preamble.tex file and subfolders for each of the chapters (Introduction, Results etc)

Thesis.tex file

This is the main file you use to compile the pdf. This is where you define the document type, the packages to use and the chapters to include in the compiled pdf.

```
\documentclass[a4paper,12pt]{report}
\textheight=24cm
\textwidth=15cm

\usepackage{fancyhdr} 		%Headers and footers
\setlength{\headheight}{15pt}
\usepackage{setspace} 		%Line settings

%\usepackage{etoolbox}
%\makeatletter
%\patchcmd{\@makechapterhead}{50\p@}{0pt}{}{}
%\patchcmd{\@makeschapterhead}{50\p@}{0pt}{}{}
%\makeatother

\usepackage{titlesec} %Load this package to reduce the white space before and after chapter heading
\titleformat{\chapter}[display]
{\normalfont\huge\bfseries}{\chaptertitlename\ \thechapter}{20pt}{\Huge}
\titlespacing{\chapter}{0pt}{0pt}{20pt} % {command}{left}{before sep} {after sep}[right] default = {0pt}{50pt}{40pt}

\usepackage{color,graphicx} %Add colour to text and further arguments for graphics
\usepackage{caption} %Subfigures over a page
\usepackage{subcaption} %Subfigures over a page
\usepackage{url} %Allows you to add urls
\usepackage{kpfonts}
\usepackage{gensymb} %Allows you to use \degree
\usepackage{tabulary} %Allows you to wrap text in a table column
\usepackage{array} %Needed for some functions in tabular
\usepackage{fixltx2e} %Allows you to use \textsubscript in tables
\usepackage{float} %Places float at precisely the location in the LaTex code
\usepackage{nameref} %Allows you to name chapter in reference rather than number
\usepackage[font=small, labelfont=bf]{caption} %Small captions in bold
\usepackage{booktabs} %Allows you to use \toprule etc when converting excel tables to latex
\usepackage{longtable, lscape} %Tables can span across multiple pages
\usepackage{tabu}
\newcommand{\ToDo}[1]{\textcolor{red}{\textsf{\textbf{#1}}}} %Creates a new command that hightlights text in red
\usepackage[titletoc,title]{appendix} %Allows partial titletoc in appendix, must be installed before hyperref package
\usepackage{titletoc} %Allows partial titletoc in appendix, must be installed before hyperref package
\usepackage[colorlinks=false]{hyperref} %Citations are turned into hypertext links
\usepackage{rotating} %Allows you to rotate floats
\usepackage{rotfloat} %Allows [H] to be used when rotating floats
\usepackage{setspace} %Set spacing in longtable
\usepackage{multirow} %Multirows in tables
\usepackage[backend=bibtex, style=authoryear, maxcitenames=2, mincitenames=1, minbibnames=10, maxbibnames=10, dashed=false]{biblatex} %References
\addbibresource{ThesisBibliography.bib} %Location of references
\renewbibmacro{in:}{} %Suppress the use of "`in"' before the journal title in bibliography
\DeclareNameAlias{sortname}{last-first} %Display all authors in bibliography as last name followed by first
\renewcommand*{\bibpagespunct}{\addcolon\space} %colon instead of comma before pages in bibliography
\AtEveryBibitem{\clearfield{number}} %remove number field from bibliography

\pagestyle{fancy} %Change the style of the current page
\renewcommand{\chaptermark}[1]{\markboth{#1}{}} %Print the name of the chapter
\renewcommand{\sectionmark}[1]{\markright{\thesection\ #1}} %Print the name of the section
\fancyhf{} %Merge of fancyfoot and fancyhead
\fancyfoot[R]{\bfseries\thepage} %Page number on bottom right
\fancyhead[L]{\bfseries\leftmark} %Current chapter printed on top left
\renewcommand{\headrulewidth}{0.5pt} %Place a line at the top of the page
\renewcommand{\footrulewidth}{0.5pt} %Place a line at the bottom of the page
\addtolength{\voffset}{-30pt} %edit individual page dimensions
\fancypagestyle{plain}{\fancyhead{}\renewcommand{\headrulewidth}{0pt}} %Create a plain page for chapter title pages

\clubpenalty=10000
\widowpenalty=10000
\hyphenpenalty=10000 %Prevent hyphenation if word is too long for line
\tolerance=2000 %How much white space is considered acceptable
\emergencystretch=10pt %Allow 10pt of additional white space per line in order to avoid underfull/overfull lines
\raggedbottom

\begin{document}
\include{Preamble}
\pagenumbering{arabic} \setcounter{page}{1}
\doublespacing
%List the subfolders and .tex files for each of the chapters to be included
\include{./Introduction/Introduction}										
\include{./Materials_and_Methods/Materials_and_Methods}		
\include{./Results1/Results1}						
\include{./Results2/Results2}									
\include{./Results3/Results3}										
\include{./Results4/Results4}										
\include{./Discussion/Discussion}									
\include{./Appendix/Appendix}										

\singlespacing
\setlength\bibitemsep{\itemsep}
\printbibliography
\addcontentsline{toc}{chapter}{Bibliography}

\end{document}
```

##### Preamble

Create a file called Preamble.tex

Use the preamble to create the following pages before the beginning of the thesis

Title page
Abstract
Acknowledgements
Declaration
Submitted abstracts
Associated publications
Other publications
Contents page
List of figures
List of tables
Abbreviations
If you want the Oxford logo for the title page, download the .pdf file from the  github repository .

```
\begin{titlepage}
   \centering
   \begin{figure}
      \centering
%      \epsfig{file=oxford_logo.eps,width=\textwidth}
      \includegraphics[scale=0.4]{oxford_logo-eps-converted-to.pdf}
   \end{figure}
   {\LARGE{\textbf{Thesis title}}}\\ 
   \vspace{2cm}
   {\Large{Candidate name}}\\
   {\Large{College}}\\
   {\Large{University of Oxford}}\\
   \vspace{2cm}   
   {\Large{\textit{A thesis submitted in partial \\ fulfilment of the requirements for the degree of\\ Doctor of Philosophy}}}\\
   {\Large{\textit{Term, Year}}}
\end{titlepage}

\newpage
\chapter*{Abstract} %Creates chapter title but doesn't number
\addcontentsline{toc}{chapter}{\numberline{}Abstract} %Add abstract to table of contents
\thispagestyle{plain}
%\pagenumbering{gobble}
%\thispagestyle{empty}
\pagenumbering{roman} \setcounter{page}{1}

%\vspace*{-1.5cm}
\begin{center}
{{\bf Thesis title}} \\
%
\end{center}
%\vspace*{-0.5cm}
\begin{center}

{Name, College, Term Year}\\
%\end{center}
%\vspace*{-0.5cm}
%\begin{center}
{A thesis submitted in partial fulfilment of the requirements
for the degree of Doctor of Philosophy of the University of Oxford} \\
%\end{center}
%\vspace*{-0.5cm}
%\begin{center}
\end{center}
%\vspace*{-0.5cm}

%\begin{center}
%{{\large \bf Abstract}}
%\end{center}

\noindent
Paragraph 1 \\

\noindent
Paragraph 2\\

\newpage
\chapter*{Acknowledgements}
\addcontentsline{toc}{chapter}{\numberline{}Acknowledgements}
\thispagestyle{plain}
%\pagenumbering{gobble}
%\thispagestyle{empty}
%\begin{center}
%{{\large \bf Acknowledgments}}
%\end{center}
\noindent
%
Acknowledgements

\newpage
\chapter*{Declarations}
\addcontentsline{toc}{chapter}{\numberline{}Declarations}
%\pagenumbering{gobble}
%\thispagestyle{empty}
\thispagestyle{plain}
%\begin{center}
%{{\large \bf Declarations}}
%\end{center}
\noindent
Declarations

\newpage
\chapter*{Submitted Abstracts}
\addcontentsline{toc}{chapter}{\numberline{}Submitted Abstracts}
\thispagestyle{plain} %Removes the header
%\begin{center}
%{{\large \bf Associated publications}}
%\end{center}
\noindent

\noindent
\textbf{Title}
\hfill \textbf{Year}\\
Authors\\

\newpage
\chapter*{Associated Publications}
\addcontentsline{toc}{chapter}{\numberline{}Associated Publications}
%\pagenumbering{gobble}
%\thispagestyle{empty}
\thispagestyle{plain} %Removes the header
%\begin{center}
%{{\large \bf Associated publications}}
%\end{center}
\noindent
\textbf{Title}\\
Journal\\
Authors\\

\begingroup
\let\clearpage\relax
\chapter*{Other Publications}
\noindent
\textbf{Title}\\
Journal\\
Authors\\

\endgroup

\newpage
\addcontentsline{toc}{chapter}{\numberline{}Contents}
\tableofcontents

\newpage
\listoffigures
\addcontentsline{toc}{chapter}{\numberline{}List of Figures}

\newpage
\listoftables
\addcontentsline{toc}{chapter}{\numberline{}List of Tables}

\chapter*{Abbreviations}
\addcontentsline{toc}{chapter}{\numberline{}Abbreviations}

\begin{table}[H]
\singlespacing
  \centering
   \begin{tabular}{@{}m{2.5cm}m{10cm}@{}}
	  \textbf{Abbreviation} & Definition \\
  \end{tabular}
	\end{table}
```

##### References

References can be exported from endnote and converted into a bibtex library format.

Within endnote select all the references (Edit, Select All) and export in Bibtex format (File, Export, Bibtex format).

Save as a text file.

Download [JabRef](http://jabref.sourceforge.net/help/EndNoteFilters.php).

Open or create a database and import the reference text file.

Select all records and click "Autogenerate Bibtex key".

Save the database as .bib with UTF-8 encoding (or other format if required).

Single name for author

For example "Wellcome Trust Case Control Consortium" place {} around the author name

Special letters

For example "Søresnen" is S{\o}rensen

##### Chapters

Create a .tex file for each chapter to be included in the thesis for example an introduction chapter	

```
\chapter{Introduction}
\label{ch:Intro}

\section{Aims and objectives}
\subsection{Specific aims}
```

##### Figures

Create a pdf for each individual figure (crop excess white space from around the figure in a pdf editor). The pdf should be in the same subfolder as the chapter.tex.

To insert a figure

```
\begin{figure}[H]
\centering
{\includegraphics[scale=0.6]{./chapter/figure.pdf}}
\caption[Title for contents page]{\textbf{Title for figure legend.} Figure legend}
\label{fig:figure.name}
\end{figure}
```

##### Tables

The [excel to latex macro](https://www.ctan.org/pkg/excel2latex) can be used to help create tables:  

##### Citing references, figures and sections

To cite a reference in the text

...(Author et al. date)

```
\parencite{AuthorDate}
```
Author et al. (date)...
```
\textcite{AuthorDate}
```
To cite a figure in the text
```
Figure~\ref{fig:figure.name}
```
To cite a chapter/section it needs to have a label (e.g \label{ch:Introduction})
```
Chapter~\ref{ch:Introduction}
```

##### Word count

To count text from latex files upload each .tex file to the following website: 
http://app.uio.no/ifi/texcount/online.php

### Other resources

[Detexify](http://detexify.kirelabs.org/classify.html) helps you find the code for a symbol

TeXnicCenter can be configured to use  Sumatra pdf reader instead of adobe. This allows forward search (double clicking on a location in the pdf automatically opens TeXnicCenter at the relevant location). See  [here](http://download2.polytechnic.edu.na/pub4/sourceforge/t/te/texniccenter/Tutorials/How_to_Sumatra_EN.pdf) for more information
