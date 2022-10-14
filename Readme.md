This is repository is for tex.stack exchange questions to be posted.


I have a custom graph paper environment, and it uses **_xparse_**'s  `\NewDocumentEnvironment` to create it. The problem is that I would like to have default arguments fed from a single optional parameter list like below:

I am using LaTeX2e (yes, i know there is a newer version, just haven't remembered to install it)

````
\documentclass{article}
\usepackage[letterpaper,landscape,top=.5in,bottom=.5in,right=.25in,left=.25in]{geometry}
\usepackage{xparse}
\usepackage{xkeyval}


\define@choicekey*{GPE}{DDD}{up,down}{down} % driagonal draw direction 
\define@key{GPE}{VLine}{Red} % vertical line color
\define@key{GPE}{HLine}{Green} % horizontal line color
\define@key{GPE}{DLine}{Blue} % diagonal line color


% #1 is optional parameters,
% #2 is x spaces
% #3 is y spaces
\NewDocumentEnvironment{CGP}{O{VLine=Red,HLine=Green,DLine=Blue,DDD=up} m m}
{
\ProcessOptionsX<GPE>
%
% ... code creating grid of coordinates

%
%Example of colors usage 
\draw[VLine](a0)--(a1);
\draw[VLine](b0)--(b1);
\draw[HLine](a0)--(b0);
\draw[HLine](a1)--(b1);


% if DDD is up
\draw[DLine](a1)--(b0);
% if DDD is down
\draw[DLine](a0)--(b1);
}
{}


\begin{document}
\begin{tikzpicture} 
\begin{CGP}[Vline=Blue,Hline=Red,DLine=Green,DDir=up]{5}{7}


\end{CGP}
\end{tikzpicture}
\end{document}

````

edit: My question is how to read a list of paramameters from a single optional parameter: `\begin{CGP}[Vline=Blue,Hline=Red,DLine=Green,DDir=u]{5}{7}`

