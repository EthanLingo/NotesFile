# Untitled


```tikz
\begin{document}
  \begin{tikzpicture}[domain=0:4]
    \draw[very thin,color=gray] (-0.1,-1.1) grid (3.9,3.9);
    \draw[->] (-0.2,0) -- (4.2,0) node[right] {$x$};
    \draw[->] (0,-1.2) -- (0,4.2) node[above] {$f(x)$};
    \draw[color=red]    plot (\x,\x)             node[right] {$f(x) =x$};
    \draw[color=blue]   plot (\x,{sin(\x r)})    node[right] {$f(x) = \sin x$};
    \draw[color=orange] plot (\x,{0.05*exp(\x)}) node[right] {$f(x) = \frac{1}{20} \mathrm e^x$};
  \end{tikzpicture}
\end{document}
```


```tikz
\usepackage{tikz-cd} \begin{document} \begin{tikzcd}     T     \arrow[drr, bend left, "x"]     \arrow[ddr, bend right, "y"]     \arrow[dr, dotted, "{(x,y)}" description] & & \\     K & X \times_Z Y \arrow[r, "p"] \arrow[d, "q"]     & X \arrow[d, "f"] \\     & Y \arrow[r, "g"]     & Z \end{tikzcd} \quad \quad \begin{tikzcd}[row sep=2.5em] A' \arrow[rr,"f'"] \arrow[dr,swap,"a"] \arrow[dd,swap,"g'"] &&   B' \arrow[dd,swap,"h'" near start] \arrow[dr,"b"] \\ & A \arrow[rr,crossing over,"f" near start] &&   B \arrow[dd,"h"] \\ C' \arrow[rr,"k'" near end] \arrow[dr,swap,"c"] && D' \arrow[dr,swap,"d"] \\ & C \arrow[rr,"k"] \arrow[uu,<-,crossing over,"g" near end]&& D \end{tikzcd} \end{document} 
```
