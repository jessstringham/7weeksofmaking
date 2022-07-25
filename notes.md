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


# Part 3

Shaders and such

## Day 11 (2022-07-17)

Started with an idea of making something generative with shaders, but ran into problems pretty quick.

Instead I really liked the [trick used in this tutorial](https://www.youtube.com/watch?v=Ms6_vBn0XQQ) to draw squares using Limit TOP's quantize. I didn't end up using the lines in my final result though: I just took a threshold on random noise.

I was thinking I could challenge myself and try mapping it to polar coordinates using the Displace TOP (heh), but [this trick](https://www.google.com/search?client=safari&rls=en&q=touchdesigner+polar+coordinates&ie=UTF-8&oe=UTF-8) of creating a tube with one opening's radius=0 seemed to work pretty well. I don't really like the blur near the edge. I tried out Texture SOP on the tube to make some fun effects, but it didn't improve the blur. I'm guessing it's because the tube's radius is (in its head) more than 1000 pixels I'm providing. I might be able to repeat the pattern. 

I fiddled with a few variations. 

I do like the effect of Blur TOP + (Displace TOP + noise) to distort + Threshold to sharpen again to make wobbly lines.

## Day 12 (2022-07-18)

I've been wanting to recreate a really cool light I saw at a bar. After learning about the Displace TOP, I've been wondering if that's all I needed. And I think it was!

I used a ramp with a period so it repeated a bunch of times, and a vertical ramp that repeated fewer times. I used the Reorder TOP to select them into Red and Blue for the Displace TOP. And amazingly, it looked about right!!

I couldn't quite get the colors to match the feeling of the original lamp, and it was very stormy in nyc, so I liked the version I made with slow-moving distorted rings. The first few seconds look like storm clouds. 

This is one of my favorites!

## Day 13 (2022-07-19)

I went back to the generative code that I use for cellular automata, but now tried adding probability to it. If I chose the right values, it would actually generate something!

After I got that working, I thought it wasn't quite interesting enough on its own.

I stacked three (completely unique) ones on top of each other, made one of them bigger, rotated all of them at an angle, and had two blue ones overlap and make a brighter blue.

## Day 14 (2022-07-20)

Excited to sit down and try for probabilistically generative images, but it was very hard to make something interesting. I was out of time, but finally had an idea for just drawing a bunch of straight lines to try to make squares of different sizes. It.. was okay. I thought to try to use it as a texture on a rotating box, which was still.. okay. Before posting I noticed the patterns on the sides of the box were very obviously not wrapping around the box, even just the three sides I was showing, bah. So I added in a wireframe of the box to make the edges not as obvious. I'll need to revisit to learn how to apply textures nicer to boxes. Also it could be cool to figure out how to make the textures actually wrap correctly.

## Day 15 (2022-07-21)

I was late to something, so I used some tests with the Ramp TOP I had done before I knew about 7weeksofmaking. I had been really surprised how cool it looked just adding a circular + vertical ramp. Since that was something I had already done, I tweaked it by fixing the format size and adding some subtle 
noise so it sparkles. #quick

## Day 16 (2022-07-22)

After setting parameters for a few generative probabilistic shaders on Day 13 and Day 14, the machine learning engineer in
me started coming up with ways to learn parameters to make interesting patterns (at least not "mostly nothing")

The first pass I did borrowed some ideas from NLP and deep learning (some of which were very likely borrowed from computer vision and computer graphics. I'm starting to love the GPU even more.) I used 2 colors (black and white) and looked at the neighboring 3 by 2 pixels in this example, but those parameters can change.

 * I run through a (single!) reference image. I love when I can work with small data.
 * Limit ("quantize") the colors a lot. The only one I have working is black and white for reasons I'll get back to below!
 * For each pixel of the image (that have enough neighbors), look at the 3 by 2 pixels above that pixel. In a counter dictionary, look at what those 3 by 2 pixels are, and add to the tally what color the current pixel is. 

Now we've taught the model what it needs to know! For each of the 64 combinations of pixel neighbors, I can extract the probability the pixel should be black or white.

To generate an image:
 * Draw enough pixels to get it started. In this case, I need 2 rows of pixels. For now, I either populate it with the first two pixels of the reference image or random noise. It's okay because there's usually a lot of randomness in this.
 * Let the shader look at the neighboring 3 by 2 pixels, and then pull up the probability. Then look at a second texture of random noise (static is fine), check if the value of that pixel is less than the probability, and then write black or white.


If you know about Markov text generation, this is the same idea! Though it's the same idea as a ton of things: generating an image line-by-line is similar to how RNNs predict sequences. Of course, it's also not far from cellular automata


I love the idea of very small data, as well as not needing to exactly be able to recreate the reference image.

I also ended up using [my stride tricks](https://jessicastringham.net/2017/12/31/stride-tricks/) blog post from a few years ago!


### The unseen, and larger spaces

So! The first version I got working with a 3 by 2 kernel and 2 colors. That leads to a space of $2^6=64$ possible pixels that I need to learn. 
In practice, these haven't been too hard for me to fill nearly all of those combinations even with small reference images. As a sane default, I can fall back to the color distribution of the entire reference image. 

So that works fine with the 64 case. But! I found that it results in chaos for larger spaces, like when I increased it to 4 colors (an example of this is worked into my actual submission for Day 16). I think this is because once one kernel is outside of the learned space, it's more likely to keep running into combinations the model has never seen before.

I have a feeling I'll be back to this problem in a bit, because I really do want to see it generate patterns that are multiple shades or use larger kernels. I'll probably throw in "just treat an unseen kernel like a nearby neighbor," or train a supervised learning model to fill in the blanks (and at that point of training a model, it is just a function so I could try out dropping that into the shader?)

The next part with larger spaces is loading the data! But hell, GPUs have to deal with image data, and my limitation of images of 1280x1280rgba still gives me 6.5M floating point numbers, which should be more than enough for my plans.


### Submission

Phew, this took a lot of coding time outside of TouchDesigner, but it's a framework I see myself experimenting with for a while longer. It wasn't quite working by the end of Day 16, so I submitted a WIP screen shot from Jupyter notebooks, adding some more fun noise using TouchDesigner. So I think it counts towards the "try to quickly make visually interesting things" tag. Also I love the idea of my work matplotlib graphs having TouchDesigner distortion on them.

## Day 17 (2022-07-23)

And I finally tracked down the bug where I wasn't looking around the grid correctly in GLSL, and it worked!

It.. looks mostly like random stuff with slightly more structure than usual. 

One thing I couldn't get working is macro-structures in the reference image. I have some ideas (I know convolutional neural networks have some tricks for this), but even easier to get a cool effect was to run the same probabilities on a lower resolution image.

*  For colors, It was a little hard not to make this just look like camouflage patterns. I colored one a magenta, another green (so they overlapped and made yellow), and set them on top of a dark blue background.
* As a final thing, I added a random chance (random noise that changes every frame) that the cell isn't generated. The kernel already requires that the above adjacent 3 cells are filled in. This made it generate a bit more slowly and with a wiggly line, which I thought looked more interesting than a straight one.
* I also cranked up the frame rate so the result is sped up a bit. Someday I'll try to limit myself to actual realtime effects, but these images take a few seconds to generate.

In TouchDesigner, I also learned how to use the `TOP To CHOP` a lot better: by default it looks like it chooses something like a row halfway down the image, but you can chnage it to select a range of rows and columns pixel values from a reference image. This was so so so useful to debug the GLSL, when I needed to look at the 2 rows being used to generate the 3rd row at specific parts of the images where things were going wrong.
(I thought I could only select specific rows, and definitely started by creating a bunch of these and merging them.)


## Day 18 (2022-07-24)

I tried a few more reference images, but the learner seems super finicky and most of the generated images look pretty similar to the cream cheese-based model (did I mention my first reference image was a picture of cream cheese?) I think I might be able to get better effects with some fiddling with image resolution and brightness. But! Even easier, I can generate a pixel pattern like straight lines or diagonal lines or a grid. The resulting model draws very cool patterns. These are my favorite things from 7weeksofmaking so far!


## Day 19 (2022-07-25)

Spoilers, but if instead of using completely random noise used to decide which route to take, I get very cool effects and I'm so happy.

