# Reference

My personal reference file where I can drop things I forget a lot.


 - TOP
   - **fit**: resize image
   - **reorder**: assign input channels to different image channels (like RGBA)
   - **lookup**: apply a colorscheme! like a ramp or noise pixels.
   - **GLSL**: oh you know it's gonna be wild

 - CHOP
   - **pattern**: gives you a little pattern, like sine and stuff
   - **merge** and **rename** can be used to make the constant of your dreams.


## GLSL


output is a vec4 of rgba.

`vec4(vec3(r), 1.0)`


pixel positions

| command | what do |
|-|-|
| `vUV.st` | position of pixel |
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

