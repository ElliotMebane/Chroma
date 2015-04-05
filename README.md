
![Chroma](http://i.imgur.com/jp31ABn.png)

`*Documentation is work in progress.*`

# Chroma
Chroma is color conversion library that implements perceptually linear color spaces such as CIELab &amp; CIE-LCH. This library borrows CIE conversions from the very popular Chroma.js JavaScript color conversion library - [Github Link](https://github.com/gka/chroma.js "Github Link")

Download it here: [Chroma](http://neil.engineer/index.php?/pages/chroma/ "Chroma")

## Motivation

Artists & designers benefit tremendously from being able to control luminosity in a linear color space. In order to conceive visual distraction, emphasis, phase, depth, importance, or an abstract artistic visual hierarchy; the ability to control luminisity is indispensible.

The human vision has evolved to prioritize luminosity information during the object recognition process. Color spaces such as **HSL**, **HSV/HSB** and **RGB** are optimized for digital displays and lack luminosity control. For example, varying Hue while keeping Saturation and Lightness constant in HSL colorspace produces perceptually non-uniform colors. Moreover, Lightness is a non-linear function of both - Saturation and Hue. This severely limits the ability to predict the apparent and perceptual luminosity.

Chroma library allows for color production in **CIE-Lab** and **CIE-LCH** (cyclindrical transfomration of CIE-Lab) which are better suited for human vision and perceptual predictibility. Chroma objects can be instantiated with CIE color parameters, but represented and drawn in RGB color space.

![alt tag](http://i.imgur.com/MnwRKHA.png)

As a demonstration, the swatches shown above exemplify the drawbacks of HSL colorspace. The top row of swatches are generated by changing the Hue `[H = {0, 72, 144, 216, 288}]` while keeping Saturation `[S = 50]` and Lightness `[L = 50]` constant. The bottom row is generated in CIE-LCH color space by setting Luminosity `[L = 80]` and Chroma `[C = 50]` while changing the Hue `[H = {0, 72, 144, 216, 288}]`. The result is a perceptually uniform palette and as a consequence, it is visually pleasant.

## Code Sample

```processing

import com.chroma.*; // Import Chroma library

int l = 50; // Luminosity, Range: 0-100
int c = 70; // Chroma, Range: 0-128
int h = 0; // Hue, Range: 0-360


Chroma testColor; // Declare a chroma object

void setup() {

    size(1280, 720);
    rectMode(CENTER);
    noStroke();

    testColor = new Chroma(ColorSpace.LCH, l, c, h, 255); // Create a chroma object
    println("Valid RGB Color: " + !testColor.clipped()); // Check if the RGB values are clipped
}

void draw() {

    background(255);


    fill(testColor.get()); // To fetch RGB color, use the getRGB method.
    rect(width/2, height/2, 100, 100); // Draw a magenta square
}
```

## API Reference

*Work in progress*

###### Color Spaces

Colors can be created or converted to one of the following color spaces:
* RGB Color Space (Default)
* HSL Color Space (Cylindrical transformation of RGB)
* HSV Color Space (Cylindrical transformation of RGB)
* LAB Color Space (CIE-Lab)
* LCH Color Space (Cylindrical transformation of CIE-Lab)


###### Constructors

```processing
// Default constructor with no arguments
Chroma testColor = new Chroma(); // Defaults to #000000 with alpha = 255

// Constructor with only 3 arguments
Chroma testColor = new Chroma(255, 0, 0); // Creates #FF0000 with alpha = 255

// Constructor with all arguments
Chroma testColor = new Chroma(ColorSpace.RGB, 255, 0, 0, 255); // Creates red

```

###### Color instantiation

```processing
// All colors below produce red (#FF0000)

Chroma testColorRGB = new Chroma(ColorSpace.RGB, 255, 0, 0, 255);
Chroma testColorHSL = new Chroma(ColorSpace.HSL, 0, 1, 0.5, 255);
Chroma testColorHSV = new Chroma(ColorSpace.HSV, 0, 1, 1, 255);
Chroma testColorLAB = new Chroma(ColorSpace.LAB, 53.24, 80.09, 67.20, 255);
Chroma testColorLCH = new Chroma(ColorSpace.LCH, 53.24, 104.55, 40.00, 255);

```

###### Get color components
```processing

// Create a magenta color in LCH color space
Chroma testColor = new Chroma (ColorSpace.LCH, 50, 70, 240, 255);

// Get RGB color
// Returns a 32-bit integer containing ARGB values
testColor.get() // #FFCB3BA1 or [255,203,59,161] 8-bits per channel

testColor.getRGB()
// Returns RGB component array: { 203.0, 59.0, 161.0 }

testColor.getHSL()
// Returns HSL component array: { 317.5, 0.5806, 0.5137 }

testColor.getHSV()
// Returns HSV component array: { 317.5, 0.7094, 0.7961 }

testColor.getLAB()
// Returns LAB component array: { 50.0,	65.7785, -23.9414 }

testColor.getLCH()
// Returns LCH component array: { 50.0, 70.0, 340.0 }

```

##### Color conversions

```processing

// RGB to LAB conversion (can be used for any color spaces);
Chroma testColorRGB = new Chroma(ColorSpace.RGB, 255, 0, 0, 255);
println(testColorRGB.getLAB()); // Prints { 53.240794589926296,	80.09245948458054,	67.203196401666}

// LCH to RGB conversion
Chroma testColorLCH = new Chroma(ColorSpace.LCH, 50, 70, 340, 255); // Creates a magenta color
println(testColorLCH.getRGB()); // Prints { 203.0, 	59.0, 	161.0 }
// Be careful when creating LAB/LCH colors. They may lie outside of the RGB color space. You can check if the color is clipped by calling the clipped() method
println(testColorLCH.clipped()); // If True: One of the R, G or B channels is clipped
```

## Tests

Chroma includes several tests & examples and they are can be loaded within the Processing IDE by clicking: `File > Examples > Library Examples > Chroma`.

Alternatively, you can find the example source code under `Processing/libraries/Chroma/examples`.

## Installation

###### How to install library Chroma


Install with the "Add Library..." tool

New for Processing 2.0: Add contributed libraries by selecting "Add Library..."
from the "Import Library..." submenu within the Sketch menu. Not all available
libraries have been converted to show up in this menu. If a library isn't there,
it will need to be installed manually by following the instructions below.


###### Manual Install

Contributed libraries may be downloaded separately and manually placed within
the "libraries" folder of your Processing sketchbook. To find (and change) the
Processing sketchbook location on your computer, open the Preferences window
from the Processing application (PDE) and look for the "Sketchbook location"
item at the top.

Copy the contributed library's folder into the "libraries" folder at this
location. You will need to create the "libraries" folder if this is your first
contributed library.

By default the following locations are used for your sketchbook folder:
For Mac users, the sketchbook folder is located inside `~/Documents/Processing`.
For Windows users, the sketchbook folder is located inside
`My Documents/Processing`.

The folder structure for library Chroma should be as follows:

```
Processing
	libraries
		Chroma
			  examples
			  library
				    Chroma.jar
			  reference
			  src
```

Some folders like "examples" or "src" might be missing. After library
Chroma has been successfully installed, restart the Processing
application.


If you're having trouble, have a look at the Processing Wiki for more
information: http://wiki.processing.org/w/How_to_Install_a_Contributed_Library

## License

The MIT License (MIT)

Copyright (c) 2015 Neil Panchal, http://neil.engineer

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
