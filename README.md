![pyrexpaint-logo](https://user-images.githubusercontent.com/9204112/150735182-551ebe2d-882e-4c46-ab44-1dcbc7cb9751.PNG)


# Details

`pyrexpaint` is a small library for loading .xp files into Python programs. So small, there is a single function provided called `load`.

An .xp file is the custom binary format used by the ASCII art editor [REXPaint](https://www.gridsagegames.com/rexpaint/index.html).

The library has no dependencies—it uses only the Python standard library (gzip, dataclasses). It supports multi-layer images, returning structured layer and tile data including ASCII codes and foreground/background RGB colors for every tile.


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

```python
import pyrexpaint
image_layers = pyrexpaint.load("hello.xp")
```

The data structure returned by `load` is as follows:

```python
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

## Accessing Tile Data

To access tiles within a layer, you can use a position helper function:

```python
import pyrexpaint
image_layers = pyrexpaint.load("hello.xp")
layer = image_layers[0]

pos = lambda x, y: x + y * layer.height
tile = layer.tiles[pos(i, j)]

# Decode the ASCII character using CP437 encoding
char = tile.ascii_code.decode("cp437")
```

## Run the Ncurses Example

```
cd ./pyrexpaint/examples
```
```
python hello-ncurses.py
```


# Use Cases

pyrexpaint is useful for:

- Loading ASCII art created in REXPaint for use in roguelike games
- Integrating REXPaint assets into Python terminal applications
- Processing and manipulating REXPaint image data programmatically


# Project Info

| | |
|---|---|
| **Author** | Matt Link |
| **License** | MIT |
| **Python** | 3.6+ |
| **Repository** | https://github.com/mattlink/pyrexpaint |
| **Bug Tracker** | https://github.com/mattlink/pyrexpaint/issues |
