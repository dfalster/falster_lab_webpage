---
title: "A nice title page for beamer presentations"
author: Daniel Falster
date: 2013-06-18
categories: [talk]
tags: [frustrations]
aliases: [/blog/2013/06/18/a-nice-title-page-for-beamer-presentations/]
---

I use [beamer](https://en.wikipedia.org/wiki/Beamer_%28LaTeX%29) for making slide
presentations, a scripted system based on the
[latex](https://en.wikipedia.org/wiki/LaTeX) markup language. Overall, I really like it.
But a persistent problem for me has been getting a pretty title page for my talks. Recently I
managed to solve this. <!-- more -->

Previously I have either used the default beamer settings, which give something
very plain, like this:

{{< figure src="../../../../notebook/2013-06-18-a-nice-title-page-for-beamer-presentations/default.png" width="500">}}

Or I edited an image in Photoshop, exported it, then loaded it into my talk as
a background. This was annoying for several reasons, but most of all the hassle
of having to fire up Photoshop every time I wanted to make a new title page, or
change my title.

I have now discovered how to make a nice title page with
- a pretty image as backgorund
- a semi-transparent text with title and author details
- clickable links to my twitter account, email address and website, using icons
from FontAwesome.

{{< figure src="../../../../notebook/2013-06-18-a-nice-title-page-for-beamer-presentations/title.png" >}}

Here's how.

# Set background image
First you need to set the background image, over-riding the default beamer
background, and dropping the beamer title and navigation symbols.

```
{
  \usebackgroundtemplate{\includegraphics[width=1.0\paperwidth]{images/Background.jpg}}
  \begin{frame}[plain]
  \end{frame}
}
```

# Overlay a text box

{{< tweet 342025944241958912 >}}

This seems like it should be relatively simple, but my first search only
uncovered large slabs of code. And my plea for help on twitter did not get any
response.

A bit more  searching yielded some answers.

- [This talk by Vesa Linja-aho](https://www.slideshare.net/linjaaho/how-to-make-
  boxed-text-with-latex) outlines several options for making framed text boxes. This
  alerted me to the framed and
  [mdframed](https://github.com/marcodaniel/mdframed) packages.
- [Here's a solution using tikz](https://tex.stackexchange.com/questions/53784/overlay-images-and-block-in-beamer), although was a bit more complicated than
  I would like.
- You can also customise the block environment, as explained
  [here](https://tex.stackexchange.com/questions/28760/custom-beamer-blocks) and
  [here](https://tex.stackexchange.com/questions/55596/how-to-make-partially-transparent-beamercolorbox)
  , including with a
  [semi-transparent or transparent background](https://tex.stackexchange.com/questions/18447/how-to-make-a-block-transparent-for-a-background-image).

In the end, my preferred option was to use the
[mdframed](https://github.com/marcodaniel/mdframed) package, as the code is
relatively concise and the package comes pre-packaged with my latex
installation. The
[user guide for mdframed](https://cloud.github.com/downloads/marcodaniel/mdframed/mdframed.pdf)
is quite good, but did not explain how to make the box transparent. That trick
is achieved using the tikz settings, as explained
[here](https://tex.stackexchange.com/questions/38281/transparent-background-for-mdframed-environment/38298#38298)
on stackexchange.

The eventual code is quite simple. Of course you need to include the mdframed package:

```latex
\usepackage[framemethod=tikz]{mdframed}

\begin{mdframed}[tikzsetting={draw=black,fill=white,fill opacity=0.7,
				 line width=4pt},backgroundcolor=none,leftmargin=0,
				 rightmargin=40,innertopmargin=4pt]
  Text in my text box
\end{mdframed}
```
or, if you prefer, you can define a new md environment

```latex
\newmdenv[tikzsetting={draw=black,fill=white,fill opacity=0.7, line width=4pt},
		backgroundcolor=none,leftmargin=0,rightmargin=40,innertopmargin=4pt]
		{titleBox}
```
and call it

```latex
\begin{titleBox}
A transparent box
\end{titleBox}
```
The above example uses the tikz options for formatting, which enables the
transparent background, but if you want a filled background, you can also use
the formatting options in mdframed:

```latex
\begin{mdframed}[outerlinewidth=3,leftmargin=0,%
				rightmargin=20,backgroundcolor=white,%
				outerlinecolor=black,innertopmargin=2pt,%
				splittopskip=\topskip,skipbelow=\baselineskip,%
				skipabove=\baselineskip]
  Text in my text box
\end{mdframed}
```
# Adding text

Beamer has a built-in command for creating title pages. If you have defined your
title, author, data and/or institution, you can use these by calling:

```latex
\begin{frame}
  \maketitle
\end{frame}
```

But that's pretty ugly. Alternatively you can

- access the elements used by   `\maketitle` directly, using the commands
`\insertdate`, `\insertauthor`, `\insertinstitute`, or `\insertshortinstitute`,
or
-  write the text yourself

# Linking to my twitter account, email and website

In addition to a text box, I also want handles to my twitter, web and email
accounts on the title page. As Hilary Mason, chief research scientist at bitly,
explains
[it is helpful to include your twitter handle](https://www.hilarymason.com/speaking/speaking-title-slides-twitter-you-win/)
so that

1. People can post you questions they didn't get to ask during the talk
2. Everyone knows you'll be watching what they say about your talk!

It turns out that it is incredibly easy to make a web link in latex :

```
\href{https://twitter.com/adaptive_plant}{@adaptive\_plant}
```

It's also relatively easy to add pretty icons, using
[FontAwesome](https://fortawesome.github.io/Font-Awesome/). On a mac, you can get
fontawesome working by following [these
instructions](https://coderwall.com/p/r67dyq). There's a couple of restrictions.

1. FontAwsome must be be installed in the system fontbook
2. You need to include the fontspec package, and use xelatek to compile your talk.

A cheatsheet of symbols available [here](https://fortawesome.github.io/Font-Awesome/cheatsheet/)

# Tweaking the location

Finally, you can move the text boxes up and down by adding some `vspace'

```latex
 \vspace{15em}
```

# Conclusion

We're done. You can find code to make this example
[here](https://github.com/dfalster/BeamerTitleSlide), as well as [compiled
pdf](https://github.com/dfalster/BeamerTitleSlide/blob/master/slides.pdf?raw=true).

{{< figure src="../../../../notebook/2013-06-18-a-nice-title-page-for-beamer-presentations/title.png" >}}

# Acknowledgements

Thanks to Rich FitzJohn for valuable discussions, showing me how to generate
make files, and reassuring me that there was no easy way to overlay text boxes
(that he knew of). Also, thanks to all the coders who posted at links listed in
this page, including of course developers of
[Latex](https://en.wikipedia.org/wiki/LaTeX) and
[Beamer](https://en.wikipedia.org/wiki/Beamer_%28LaTeX%29), which despite their
troublesome nature, still remain best option (IMO) for making presentations.

