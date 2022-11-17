[Back to Readme](README.md)

### Fontawesome
* Fontawesome is a font that has many symbols like phone, location, envelope, LinkedIn, Bluetooth etc.
* Example to use the map marker (location pin): the command \faMapMarker from the package fontawesome :  
```
\documentclass{scrartcl}
\usepackage{fontawesome}

\begin{document}
Map Symbol: \faMapMarker
\end{document}
    
```

### Images

* Put a picture in front of text in LaTeX - using tikz

```
\usepackage{tikz}


\begin{tikzpicture}[remember picture,overlay]
    \node[xshift=65mm,yshift=-48mm,anchor=north west] at (current page.north west){%
    \includegraphics[width=50mm]{example-image-a}};
\end{tikzpicture}
```
[Source](https://tex.stackexchange.com/a/377083)

[Back to Readme](README.md)