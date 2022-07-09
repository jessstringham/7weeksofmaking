# Day 1

Trying the cellular automata on magnetic spheres. 

Spheres have one black and one white hemisphere. Rotating them changes the color, 
but you get little phases in between. Cute!

(this was.. very badly misremembering how e-ink works lol. I remembered magnets and 
ball and colors).

I'm using eh.vie's tutorial on Instanced Geometries to set up the little spheres.
For a while, I thought I couldn't use this because TD would crash when I tried, but
as long as I use it carefully, TD doesn't crash. **Learning: save all the time**

 * Use `reorder` to combine two ramps to easily set up a TOP that can be used to to place objects uniformity. Wicked!
 * Use Common > Viewer Smoothness > Nearest Pixel to make things look like squares. I think the data still gets passed through, but the viewer looks less blurry.
 * **Subtle Learning: when things are going wrong between TOP and Geo, double check your Pixel Format!* 32-bit float usually works.


Made rgb noise, and each control a rotational axis. (I might be missing one color because 
one rotational axis is rotating the sphere not-against-a-color-hemisphere.

For noise like "Simplex 3D (GPU)", using `absTime.seconds * [some fraction]` in a noise's Transform > Translate value 
makes a nice smooth change. Will have to try out a bunch of noises.

## Day 2

Conveniently, this person gave [a tutorial](https://www.youtube.com/watch?v=VBzIPLh-ECg&t=1693s)
on basically exactly what I wanted! So I ventured into GLSL shaders. This reference is useful too: [Write a GLSL Top](https://docs.derivative.ca/Write_a_GLSL_TOP).

But, I ran into the problem some folks in the audience
also did: it was all black. But back at it for Day 2!

Trying to debug the GLSL was weird, since I don't know how to use print statements. But instead:
 * Use a `TOP to` CHOP, and then a `CHOP to` DAT, to print out a table of data. 
 * Then go back to the script and start setting `fragColor` to what value.. you're trying to print.
 * Figure out a row in the table that corresponds to some troubleshome spot, and see what values are being produced.
 * Do gymnastics in your head to figure out what that means.


# Ideas for future practice days

Adding things here as they come up.


 * exploration day: play with all the types of noise, and the parameters there.
 * exploration day: feedback loops with adds, transforms, composites.

 * documentation: make a cheat sheet for the feedback loop and render network. I need to learn more tricks there!






Started trying GLSL shader following 
