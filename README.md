BooleanOperations
=================

Boolean operations on paths based on a super fast [polygon clipper library by Angus Johnson](http://www.angusj.com/delphi/clipper.php).

To compile the cpp wrapper [cython](http://cython.org) is required.

    python setup.py build_ext --inplace


A note on `setup.py`
------------

The included `setup.py` file operates in one of two modes depending on whether or not the file `dev` is present in the project root directory.

If the file is present -- i.e., "development mode", as in the Github repository --, [Cython](http://cython.org/) is required to convert the `.pyx` files to `.cpp`.

If the `dev` file is not present -- i.e., "distribution mode" --, then no Cython is required and the pre-generated `.cpp` files contained in the source distribution are used.

Of course, in both cases a C++ compiler is needed to build the Python extension module.

This mechanism allows source distributions to be installed on systems which don't have Cython or have a different versions.

The idea comes from <https://github.com/MattShannon/bandmat>. 

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
