# Week 1 (2022-07-07)

Some favorite OPs that I usually forget

 - TOP
   - **fit**: resize image
   - **reorder**: assign input channels to different image channels (like RGBA)
   - **lookup**: apply a colorscheme! like a ramp or noise pixels.
   - **GLSL**: oh you know it's gonna be wild

 - CHOP
   - **pattern**: gives you a little pattern, like sine and stuff
   - **merge** and **rename** can be used to make the constant of your dreams.
   - 


## Day 1 (2022-07-07)

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

## Day 2 (2022-07-08)

Conveniently, this person gave [a tutorial](https://www.youtube.com/watch?v=VBzIPLh-ECg&t=1693s)
on basically exactly what I wanted! So I ventured into GLSL shaders. This reference is useful too: [Write a GLSL Top](https://docs.derivative.ca/Write_a_GLSL_TOP).

But, I ran into the problem some folks in the audience
also did: it was all black. But back at it for Day 2!

Trying to debug the GLSL was weird, since I don't know how to use print statements. But instead:
 * Use a `TOP to` CHOP, and then a `CHOP to` DAT, to print out a table of data. I think this only does 1 line per row though.
 * Then go back to the script and start setting `fragColor` to what value.. you're trying to print.
 * Figure out a row in the table that corresponds to some troubleshome spot, and see what values are being produced.
 * Do gymnastics in your head to figure out what that means.

## Day 3 (2022-07-09)

shh, this was actually at 2am on Saturday. Had a busy day!

I wanted the spheres to rotate visably. I also wanted them to only ever rotate in one direction, so it didn't matter if it was going black to white or white to black, it'll be rotating down.

So the trick was: instead of setting each pixel to 0 or 1, I had "around 0 or 1" be black, and "around 0.5" mean white. It then checks if the pixel was around the color it was supposed to be, and snaps to 0 or 0.5 if it is. If not, increment the pixel value by the fraction I wanted them to rotate. If the number was above 1.0 I would subtract 1.0. 
The next row would wait until the pixel above was the right color before triggering any change. Phew.

I kinda hope there are edge cases where the pixels get stuck, or some columns change before others. Maybe I can try introducing them!

Also, my vision was for them to always rotate down, which is also the direction the image updates. But! When I did this, the effect kinda just looked like I was dragging a rectangular mask straight down! You couldn't really tell how the spheres were actually rotating. So I played with which axis to rotate, just so it was clear the spheres were actually rotating.

I think that wraps up the main goal of this first little project. 
In the next few weeks, I might try to display other things using the same setup (text?), or apply filters. But mostly I'll let it rest.

Also a thought, I've been numbering them a day later than other folks doing it. One of these days I'll post two and realign with others I think.

## Day 4 (2022-07-10)

Today I just tried a bunch of video effects. It was my first time doing things like that to regular videos.
Most looked kinda weird and didn't quite look the way I wanted them to.

I tried out turning an image black-and-white, and then applying a lookup to make some weirder color combinations.

I also tried using an image to adjust some line positions. That was kind of cool. But when I tried tubes, it was way too heavy for my computer, and lines were a little too thin to even notice.

Today I also figured out how to split my screen and show a preview in a Panel (display what's in an `out` operator). Because as cool as it looks to have the preview right behind your screen, it was making it hard to see my operators!


## Day 5 (2022-07-11)

I had one more idea for the moon shapes that I wanted to do before wrapping up some project post about them.




# Ideas for future practice days

Adding things here as they come up.


 * exploration day: play with all the types of noise, and the parameters there.
 * exploration day: feedback loops with adds, transforms, composites.

 * documentation: make a cheat sheet for the feedback loop and render network. I need to learn more tricks there!

 * i really want to try applying lookups to random images! [like in this one](https://www.youtube.com/watch?v=mAp_wxuuw_U&t=698s)
 * now that i've done glsl, what weird affects can i do? i had to do motion blur in feedback..


 * how can i create a color scheme? I know how to make a 1x5 random noise, but I don't know how to 
 * how do folks manage constants that are used in a ton of places? there are so many little lines!
