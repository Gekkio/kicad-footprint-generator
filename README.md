# kicad-footprint-generator

This repository contains a script to generate kicad footprints using python

### example

```python
from kicad_mod import KicadMod, createNumberedPadsTHT

footprint_name = "example_footprint"

# init kicad footprint
kicad_mod = KicadMod(footprint_name)
kicad_mod.setDescription("A example footprint")
kicad_mod.setTags('example')

# set general values
kicad_mod.addReference('REF**', {'x':0, 'y':-3}, 'F.SilkS')
kicad_mod.addValue(footprint_name, {'x':1.5, 'y':3}, 'F.Fab')

# create silscreen
kicad_mod.addRectLine({'x':-2, 'y':-2}, {'x':5, 'y':2}, 'F.SilkS', 0.15)

# create courtyard
kicad_mod.addRectLine({'x':-2.25, 'y':-2.25}, {'x':5.25, 'y':2.25}, 'F.CrtYd', 0.05)

# create pads
createNumberedPadsTHT(kicad_mod, 2, 3, 1.2, {'x':2, 'y':2.6})

# output kicad model
print(kicad_mod)
```

# kicad_mod_tree (next gen kicad module generator) (currently under development)

Currently, I'm working at kicad_mod_tree which is using a render tree to construct the model.

Advantage for example is simple usage of transformation operations like rotation and translation on the full (or a part) of the footprint.
Furthermore, we are able to copy complex structures of the footprint and later transform them in any way you want.

### example

```python
from kicad_mod_tree import *

kicad_mod = KicadMod("Test")
kicad_mod.setDescription("some description")
kicad_mod.setTags("test")

# set general values
# TODO

# create silscreen
kicad_mod.append(RectLine(start=[-2,-2], end=[5,2], layer='F.SilkS', width=0.15))

# create courtyard
kicad_mod.append(RectLine(start=[-2.25,-2.25], end=[5.25,2.25], layer='F.CrtYd', width=0.05))

# create pads
# TODO

# output kicad model
print(kicad_mod)
```