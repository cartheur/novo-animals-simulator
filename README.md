# novo animals simulator
A simulator for the interaction of TTL chips as conjoined SVG images.

This is an interesting approach to solve design problems before wirewrapping pins together, creating SVG images for TTL chip diagrams. Basically, its an SVG, why not make it interactive? The graphics source is a DXF made with librecad, the text height is 5.2mm (important detail for modifying it), converted and automated the diagram with inkscape. (javascript) There are some things that could be improved, for example, due to the layers used, the text ON the pins is not clickable, and will steal clicks on your pins to change the state.

## How it works

The *input* pins of the chip can be clicked to change their state. During the state change, the ouput pins are updated by amalgamating the input pins into an index, and using a lookup table to determine what the outputs should be, then going thru all the outputs and correcting their states. Because this uses a lookup table, dropping function tables in for any other chip should be easy. Use the included C-PLD software to generate tables.

In Inkscape, click on an interactive area and set the 'interactive' 'onclick' handler as required, I created two functions, clickOn, and clickOff, which reffer to turning the coloured layers on and off. When the layer is off, the pin is high (default red) when the layer is on a green box is overlaid on the red to make it green (low). Because that's a bit messed up, I created PinHigh and PinLow functions. there is IsHigh() that will tell you the current state of a pin as well.

Under file, you can go to document properties and under that go to scripts, which contains "script 5004" or something like that, which is the main set of functions for the whole thing. This can be extended to sets of TTL designs. Layer names: yeah inkscape. nowhere in the SVG do the layer names actually seem to exist, they do not go by the name of the layer *in* Inkscape, but the layer number. This is why there is an offset-by one after pin 7, becasue I did not make a layer for pin 8, as its ground. Expect confusing fun there. A correction will be found in due course.

## A working demonstration

For a working demo (exact same file as here), you can use 
  http://ruemohr.org/~ircjunk/programming/74xx138-IA.svg

  Please take and modify this into other chips.