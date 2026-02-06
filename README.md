![pyrexpaint-logo](https://user-images.githubusercontent.com/9204112/150735182-551ebe2d-882e-4c46-ab44-1dcbc7cb9751.PNG)


# Details
`pyrexpaint` is a small API for loading .xp files into python programs. So small, there is a single function provided called `load`.

An .xp file is the custom binary format used by the ASCII art editor [REXPaint](https://www.gridsagegames.com/rexpaint/index.html).


# About REXPaint

[REXPaint](https://www.gridsagegames.com/rexpaint/index.html) is a free ASCII art editor from [Grid Sage Games](http://www.gridsagegames.com/). It's commonly used for roguelike mockups, game UI layouts, and ANSI art.

## Features

- Edit characters, foreground, and background colors separately
- Multi-layer support
- True-color RGB/HSV/hex color picker
- Custom fonts, extended characters, and tilesets
- Export to PNG, ANS, TXT, CSV, XML, and `.xp` (compressed)

## Platform

Windows-only, but works under Wine on Linux and macOS.


# Installation


```
pip install pyrexpaint
```

or install from source:

```
git clone https://github.com/mattlink/pyrexpaint
```
```
pip install ./pyrexpaint
```

# Usage

Say you have an .xp file `hello.xp` in the same directory as your program, it can be loaded using:
```
import pyrexpaint
image_layers = pyrexpaint.load("hello.xp")
```

The data structure returned by `load` is as follows:
```

@dataclass
class Tile:
    ascii_code: str
    fg_r: str
    fg_g: str
    fg_b: str
    bg_r: str
    bg_g: str
    bg_b: str


@dataclass
class ImageLayer:
    width: int
    height: int
    tiles: List[Tile]


def load(file_name: str) -> List[ImageLayer]:
    ...
```


## Run the Ncurses Example:

```
cd ./pyrexpaint/examples
```
```
python hello-ncurses.py
```

