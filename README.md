# pd-gears
OpenSCAD involute parametrized gear generator

Based on project by Leemon Baird http://www.thingiverse.com/thing:5505 with some minor
and major API fixes and improvements.

Version 1.1 is total copy of publicDomainGearV1.1.scad from thingiverse project,
modifications start from 2.x.

Major changes in 2.x:
- add 'center' [true/false] param to gear and rack modules to decide if gear or rack should be centered by z axis, don't center by default
- add $fn param to gear module to control number of fragments when render hole cylinder, $fn=20 by default
+ minor internal code fixes and improvements

Description from Leemon Baird original project:

Public Domain Parametric Involute Spur Gear (and involute helical gear and involute rack)
version 1.1
by Leemon Baird, 2011, Leemon@Leemon.com
http://www.thingiverse.com/thing:5505

This file is public domain.  Use it for any purpose, including commercial
applications.  Attribution would be nice, but is not required.  There is
no warranty of any kind, including its correctness, usefulness, or safety.

This is parameterized involute spur (or helical) gear.  It is much simpler and less powerful than
others on Thingiverse.  But it is public domain.  I implemented it from scratch from the 
descriptions and equations on Wikipedia and the web, using Mathematica for calculations and testing,
and I now release it into the public domain.

		http:en.wikipedia.org/wiki/Involute_gear
		http:en.wikipedia.org/wiki/Gear
		http:en.wikipedia.org/wiki/List_of_gear_nomenclature
		http:gtrebaol.free.fr/doc/catia/spur_gear.html
		http:www.cs.cmu.edu/~rapidproto/mechanisms/chpt7.html

The module gear() gives an involute spur gear, with reasonable defaults for all the parameters.
Normally, you should just choose the first 4 parameters, and let the rest be default values.
The module gear() gives a gear in the XY plane, centered on the origin, with one tooth centered on
the positive Y axis.  The various functions below it take the same parameters, and return various
measurements for the gear.  The most important is pitch_radius, which tells how far apart to space
gears that are meshing, and adendum_radius, which gives the size of the region filled by the gear.
A gear has a "pitch circle", which is an invisible circle that cuts through the middle of each
tooth (though not the exact center). In order for two gears to mesh, their pitch circles should 
just touch.  So the distance between their centers should be pitch_radius() for one, plus pitch_radius() 
for the other, which gives the radii of their pitch circles.

In order for two gears to mesh, they must have the same mm_per_tooth and pressure_angle parameters.  
mm_per_tooth gives the number of millimeters of arc around the pitch circle covered by one tooth and one
space between teeth.  The pitch angle controls how flat or bulged the sides of the teeth are.  Common
values include 14.5 degrees and 20 degrees, and occasionally 25.  Though I've seen 28 recommended for
plastic gears. Larger numbers bulge out more, giving stronger teeth, so 28 degrees is the default here.

The ratio of number_of_teeth for two meshing gears gives how many times one will make a full 
revolution when the the other makes one full revolution.  If the two numbers are coprime (i.e. 
are not both divisible by the same number greater than 1), then every tooth on one gear
will meet every tooth on the other, for more even wear.  So coprime numbers of teeth are good.

The module rack() gives a rack, which is a bar with teeth.  A rack can mesh with any
gear that has the same mm_per_tooth and pressure_angle.

Some terminology: 
The outline of a gear is a smooth circle (the "pitch circle") which has mountains and valleys
added so it is toothed.  So there is an inner circle (the "root circle") that touches the 
base of all the teeth, an outer circle that touches the tips of all the teeth,
and the invisible pitch circle in between them.  There is also a "base circle", which can be smaller than
all three of the others, which controls the shape of the teeth.  The side of each tooth lies on the path 
that the end of a string would follow if it were wrapped tightly around the base circle, then slowly unwound.  
That shape is an "involute", which gives this type of gear its name.

