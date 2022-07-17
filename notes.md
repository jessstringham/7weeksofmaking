# Part 1 (2022-07-07 to 2022-07-11)

For the first few days, I was still forming what I wanted out of the project. 

When starting with a new tool/programming language/etc, I don't know what's natural. My favorite way is to give myself some idea I think I might be able to create in the program, and then figure out how to create something like it.

I also needed to sort out my workflow for creating, exporting, and uploading: 
 * Set the resolution to 1024x1024.
 * Everytime I make something somewhat cool, I zoom out to the project area, and copy and paste the project before tweaking it more.
 * When I have something I might publish,:
   * I uncheck the Realtime thing
   * record a video in a "Movie File Out" TOP for a few seconds.
   * Rename the file
   * airdrop it to my phone and finish cutting the timeline (funny that's easier on my phone!). 
   * And post as a story to instagram.

I'm planning to make posts on instagram with a bunch of days from similar themes. And I'll put them on my blog too once I get that running again!

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

I tried adding text to the rotation! I ended up doing way too much math in nodes, though now I think I can just add it to constants. I also was trying to use feedback to do something when I probably could have just adjusted the transparency.

# Part 2 (2022-07-12 to 2022-07-16)

I was hosting for a few days, so I didn't want to spend too long heads-down on a geometry problem or a GLSL shader or MIDI controllers. So I stuck a lot more with TOPs, which give visual feedback. I think these will be useful tricks I could do later on too!

## Day 6 (2022-07-12)

Today is the first day where I don't have much time! So let's do something quick.

This one I ended up doing only in TOPs, of a circle with some noisy horizontal lines cut out of it. I'm also trying to add some gradients and noise.

## Day 7 (2022-07-13)

For this day, I wanted to experiment with motion to prepare for a project I want to do in the next few weeks.

One idea I had was that I could generate a strip of new material, offset the image by the same amount, and composite those together. Then use feedback loops to keep looping repeating. To start with I used random noise.

Honestly, the first results made us dizzy, so I tried a few things:
 * I generate a narrower strip than I intended and then using the Fit TOP to stretch the noise horizontally, and applying a Blur TOP to the result.
 * I got some advice to try some different colors for the noise (using my current favorite trick of a Lookup TOP): high-contrast colors gave a different effect than colors that were similar!

Eh, but that's not a cool visual, so I added a polygon, and applied a different level of blur to the polygon vs the background.

We also created this wicked effect where it looked like a cylinder of thread rolling down a carpet. That was unexpected and pretty cool.

## Day 8 (2022-07-14)

We went to the Guggenheim, so I tried to recreate some little effects from Kandinsky. I liked taking a Ramp TOP x Noise TOP (random), of the same shape, but slightly offset.

## Day 9 (2022-07-15)

I did some simple Instanced Geometry in this one: I created a rotating line (like a clock face) and marked the line with little circles. Then I used feedback to create a trail, and a threshold to limit the length of the trail. I was somewhat thinking of planets rotating.

For some reason, there's this weird line that follows the circles around from the feedback. I'll get to the bottom of it one day.

And then the Displace TOP! It feels like it was inevitable that I'd start using the Displace TOP (whenever you create a new project, there's a Diplace TOP there). In this case, I just applied a little noise, and then started reading up on what it was doing.

I liked the result: it's like a tree trunk sonar.

## Day 10 (2022-07-16)

I did a few more experiments with the Displace TOP that I didn't post, but it was pretty fun. [This post](https://forum.derivative.ca/t/explaining-the-displace-top/152892) on the Forum was super super useful, and I started experimenting with my own simple displacement inputs. It's really wicked to think about using image data to instruct how to change another image, and I wonder if I can do some fun tricks there. I also love the parallels with using images as input into Instanced Geometry.

In the end, my post was another "Noise as displace input". I took a ramp with a short period, which create lots of repeating gradients, and just used some noise to displace it. I thought the effect was cool without too much thinking.
