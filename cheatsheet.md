# Reference

My personal reference file where I can drop things I forget a lot.

select a top and press Alt+N to create a null OP!!

in the menu, hold down shift to keep the window open (TODO I think this one tries to connect nodes, not sure how to prevent that)

right click on parameters, like resolution, and copy. then you can paste in others to reuse the parameters. (though then all of yours will be connected to that node)


 - TOP
   - **fit**: resize image
   - **reorder**: assign input channels to different image channels (like RGBA)
   - **lookup**: apply a colorscheme! like a ramp or noise pixels.
   - **GLSL**: oh you know it's gonna be wild
   - **Analyze**: can compute things like "count number of pixels that aren't transparent"!

 - CHOP
   - **pattern**: gives you a little pattern, like sine and stuff
   - **merge** and **rename** can be used to make the constant of your dreams.
   - **Info** get information about an image


## some useful youtube videos

 - [Turning a Geometry into DAT and back!](https://www.youtube.com/watch?v=5DRlPjdirHg)
 - [This one about UV Unwrapping](https://www.youtube.com/watch?v=HPun50ej4W8&t=538s) is useful for Geometry GLSLs.


## TScript

| command | what do |
|-|-|
| `op('constant1').par.alpha = float(op('pixelColor')[0,0])` | read in from a DAT table and set the alpha of a constant TOP |

## GLSL


output is a vec4 of rgba.

`vec4(vec3(r), 1.0)`

you probably want 32-bit float.


pixel positions

| command | what do |
|-|-|
| `vUV.st` | position of pixel |
| `vec2 pixelLoc = vUV.st * uTD2DInfos[0].res.ba - vec2(0.5, 0.5);` | make positions like actual pixels. be careful with rounding! |
| `vUV.st + vec2(x, y) * uTD2DInfos[0].res.xy;` | position of pixel that is moved by x and y pixels |



Get things about input image:

change `[0]` to others to access multiple inputs

| command | what do |
|-|-|
| `texture(sTD2DInputs[0], uv)` | get pixel of input image |
| `uTD2DInfos[0].res` | resolution of input img |




 - shadertoy and [Inigo Quilez's blog](https://iquilezles.org/articles/) can be useful


### Displace TOP

by default, 0.5 means don't move, 0.0 and 1.0 will move (the size of the canvas?). Red moves horizontally, Blue vertically (TODO: double check i have that right.)
Can create two grayscale images that describe how to move things vertically and horizontally and then use Reorder to create the image to displace by.


### SOPs

SOPs are on the CPU and can affect realtime.

 - w :: shows wireframe
 - p :: shows little dialog, so you can show normals and such

SOP to DAT will give you all the info you need.

One trick is to move calculations out into TOPs. Wild.

Normals figure out which direction the face is facing, and help the textures and lighting look better. Someday I'll understand how to do funny stuff with this.


### channel selection stuff

 - `t[xyz]` :: `tx ty tz`
	

### etc

 - Info CHOP is useful for getting image resolutions

