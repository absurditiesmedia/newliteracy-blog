---
publishDate: "20 January 2025"
title: Defining New ASCII Designs For Thomas Jensens Boxes Software
description: GNU Boxes is one of a handful of great ASCII art utilities for linux released under the GPL. 
tags: ["GPL", "linux", "cli", "foss", "ascii art"]
coverImage:
    src: "../../assets/newlit-ascii-large.png"
    alt: "newliteracy business card image passed through letterpress then displayed in the terminal "
---

The Boxes command line tool takes a block of text and wraps it in one of 50 some frames listed with `boxed -l` and specified by the user with `boxes -d` the text can either be piped into boxed or a file containing the text may be passed as as an argument `cat <file> | boxes -d <design>` or `boxes -d <design> <file>`. If you're like me, you can resist the urge to create an ascii design when prompted so, I've written this quick guide to help you understand how it all works.


Here's an example from the file `boxes-config` located in `$HOME/.config/boxes/boxes-config` new designs can be added to the end of this file:

```bash
BOX doublelinebox
author  "Rick Pfahl"
designer "(public domain)"
tags    ("simple","programming","box")
sample
        ╔══════════════════════════════════════╗
        ║                                      ║
        ╚══════════════════════════════════════╝
ends
shapes {
  nw("╔")  n("═")  ne("╗")
   w("║")           e("║")
  sw("╚")  s("═")  se("╝")
}

delim ?"

padding {
        horiz 2
        vert 1
        }
elastic(n,s,e,w)
END doublelinebox
```

The first few lines are self-explanatory. Next comes the `sample` followd by an ascii sample of the box to wrap the provided text. You should create this first because it will be easy to copy / paste the components into the `shapes` section. End the sample with `ends` on its own line and you'll be ready for the complicated part. This example doesn't show it, but there are several constraints on what the values can be. 

1) Values in the same **ROW** need to have the **same vertical height** (they need to contain the same number of rows).
     So if **NW** is *5 rows high*, then **N** and **NE** must also be *5 rows high*. 
2) values in the same **COLUMN** need to have the **same number of characters**. 
     That means if **NW** is *5 characters wide*, so must **W**, and **SW** be *5 characters wide*. Same goes for **NE**, **E**, and **SE** *as a set*. Those are the only constraints.

further down the config you'll find **padding** this is pretty self explanitory, this is how many rows or columns will be added around the text supplied to boxes before adding the frame.

Next you'll find the elastic function, this will specify which sides will be elastic, you'll notice as **N,S,E,W** are set, **N** doe not need to match the dimensions of **S** and **W** doe not need to match the dimensions of **E**.

The configuration of a box is complete with the addition of END <designmame> to match the BOX <designname> at the top.

Here's another more complicated example. Notice how multiple rows are defined as a list of comma delimited, double-quote enclosed strings:
```bash
BOX gradientbox
author "Rick Pfahl"
designer "(public domain)"
tags ("simple","programming","box")

sample 
█████████████████████████████████████████
█▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓█
█▓▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▓█
█▓░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░▓█
█▓░                                   ░▓█   
█▓░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░▓█
█▓▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▓█
█▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓█
█████████████████████████████████████████ 
ends

shapes {
  nw("███","█▓▓","█▓▒","█▓░")  n("█","▓","▒","░")  ne("███","▓▓█","▒▓█","░▓█")
   w("█▓░")                                                           e("░▓█")
  sw("█▓░","█▓▒","█▓▓","███")  s("░","▒","▓","█")  se("░▓█","▒▓█","▓▓█","███")
}
 
delim ?"

padding { 
        horiz 2 
        vert 1 
}
 
elastic(n,s,e,w)

END gradientbox
```

Additional documentation can be found on the offical website of the project at:

- [Boxes Command line ASCII boxes unlimited!](https://boxes.thomasjensen.com/)

If you're interested in creating ASCII Art, I'm sure you'll find the following list of links useful:

- [ASCII Draw](https://github.com/Nokse22/ascii-draw)
- [DurDraw](https://github.com/cmang/durdraw): Unicode, ASCII, ANSI Color art editor for UNIX type system command line interface
- [ArtTime](https://github.com/poetaman/arttime): ASCII ART Gallery of 500+ images and growing
- FONTS [CFONTS](https://github.com/dominikwilkowski/cfonts) | [FIGLET Fonts](github.com/xero/figlet-fonts)
- [GITHUB TAG ASCII-ART](https://github.com/topics/ascii-art)
