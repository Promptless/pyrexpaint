![pyrexpaint-logo](https://user-images.githubusercontent.com/9204112/150735182-551ebe2d-882e-4c46-ab44-1dcbc7cb9751.PNG)


# Details
`pyrexpaint` is a small API for loading .xp files into python programs. So small, there is a single function provided called `load`.

An .xp file is the custom binary format used by the ASCII art editor [REXPaint](https://www.gridsagegames.com/rexpaint/index.html).


# About REXPaint

[REXPaint](https://www.gridsagegames.com/rexpaint/index.html) is an ASCII art editor developed by Grid Sage Games. It's popular in the roguelike game development community for creating tile-based artwork, UI mockups, and ASCII graphics. REXPaint supports multiple layers, a full palette of foreground and background colors, and exports artwork to its native `.xp` format.


# The .xp File Format

The `.xp` format is REXPaint's native binary file format. Files are gzip compressed and support multiple image layers. Each tile stores an ASCII character code (using CP437 encoding) plus foreground and background RGB color values. Integer values use little-endian byte ordering.


# Use Cases

`pyrexpaint` lets you load REXPaint ASCII art into Python programs—handy for roguelike games, terminal applications, or rendering with ncurses.


# Requirements

Python 3.6+ with no external dependencies (just uses `gzip`, `typing`, and `dataclasses` from the standard library).


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

