BooleanOperations
=================

Boolean operations on paths based on a super fast [polygon clipper library by Angus Johnson](http://www.angusj.com/delphi/clipper.php).

You can download the latest version from PyPI:

<https://pypi.org/project/booleanOperations>.

Install
-------

[Pip](https://pip.pypa.io/en/stable/) is the recommended tool to install booleanOperations.

To install the latest version:

```
pip install booleanOperations
```

BooleanOperations depends on the following packages:
- [pyclipper](https://pypi.org/project/pyclipper/): Cython wrapper for the C++ Clipper library
- [fonttools](github.com/behdad/fonttools)
- [ufoLib](https://github.com/unified-font-object/ufoLib)

As of September 2016, only pyclipper is available on PyPI and therefore installed automatically with booleanOperations. The fonttools version 3.0 available from PyPI is too old, whereas ufoLib simply is not on PyPI yet, hence you need to install them separately.

You can use pip to install them from the respective git repositories:

```
pip install git+https://github.com/behdad/fonttools.git
pip install git+https://github.com/unified-font-object/ufoLib.git
```

BooleanOperationManager
-----------------------

Containing a `BooleanOperationManager` handling all boolean operations on paths. Paths must be similar to `defcon`, `robofab` contours. A manager draws the result in a `pointPen`.

    from booleanOperations import BooleanOperationManager
    
    manager = BooleanOperationManager()

    
### BooleanOperationManager()

Create a `BooleanOperationManager`.

#### manager.union(contours, pointPen)

Performs a union on all `contours` and draw it in the `pointPen`.
(this is a what a remove overlaps does)

#### manager.difference(contours, clipContours, pointPen)

Knock out the `clipContours` from the `contours` and draw it in the `pointPen`.

#### manager.intersection(contours, clipContours, pointPen)

Draw only the overlaps from the `contours` with the `clipContours`and draw it in the `pointPen`.

#### manager.xor(contours, clipContours, pointPen)

Draw only the parts that not overlaps from the `contours` with the `clipContours`and draw it in the `pointPen`.

#### manager.getIntersections(contours)

Returning all intersection for the given contours

BooleanGlyph
------------

A glyph like object with boolean powers.

    from booleanOperations.booleanGlyph import BooleanGlyph
    
    booleanGlyph = BooleanGlyph(sourceGlyph)

### BooleanGlyph(sourceGlyph)

Create a `BooleanGlyph` object from `sourceGlyph`. This is a very shallow glyph object with basic support.

#### booleanGlyph.union(other)

Perform a **union** with the `other`. Other must be a glyph or `BooleanGlyph` object.
    
    result = BooleanGlyph(glyph).union(BooleanGlyph(glyph2))
    result = BooleanGlyph(glyph) | BooleanGlyph(glyph2)

#### booleanGlyph.difference(other)

Perform a **difference** with the `other`. Other must be a glyph or `BooleanGlyph` object.

    result = BooleanGlyph(glyph).difference(BooleanGlyph(glyph2))
    result = BooleanGlyph(glyph) % BooleanGlyph(glyph2)

#### booleanGlyph.intersection(other)

Perform a **intersection** with the `other`. Other must be a glyph or `BooleanGlyph` object.

    result = BooleanGlyph(glyph).intersection(BooleanGlyph(glyph2))
    result = BooleanGlyph(glyph) & BooleanGlyph(glyph2)

#### booleanGlyph.xor(other)

Perform a **xor** with the `other`. Other must be a glyph or `BooleanGlyph` object.

    result = BooleanGlyph(glyph).xor(BooleanGlyph(glyph2))
    result = BooleanGlyph(glyph) ^ BooleanGlyph(glyph2)

#### booleanGlyph.removeOverlap()

Perform a **union** on it self. This will remove all overlapping contours and self intersecting contours.

    result = BooleanGlyph(glyph).removeOverlap()

----

#### booleanGlyph.name

The **name** of the `sourceGlyph`.

#### booleanGlyph.unicodes

The **unicodes** of the `sourceGlyph`.

#### booleanGlyph.width

The **width** of the `sourceGlyph`.

#### booleanGlyph.lib

The **lib** of the `sourceGlyph`.

#### booleanGlyph.note

The **note** of the `sourceGlyph`.

#### booleanGlyph.contours

List the **contours** of the glyph.

#### booleanGlyph.components

List the **components** of the glyph.

#### booleanGlyph.anchors

List the **anchors** of the glyph.
