---
# stuff
theme: ./theme
info: a
title: Using Godot for mixed-reality livestreaming
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
---

# Using Godot for mixed-reality livestreaming

Godotcon Boston 2025

<img src="/title.png" class="w-70 absolute bottom-0 right-0" style="filter:drop-shadow(0 0 20px #537fff88);" />

<!--
good luck

TODO: make this slide better
-->

---

# what does that mean

`mix(real_camera, virtual_camera, 0.5)`

<div class="relative flex items-center justify-center">
  <img src="/Camera3D.svg" width="250px" class="object-contain" />
  <span class="text-9xl ml-5 mr-10">+</span>
  <img src="/sony.png" width="250px" class="mt-20 object-contain" style="filter:drop-shadow(0 0 8px #777);" />
</div>

---
layout: image
---

# what does that mean

`mix(real_camera, virtual_camera, 0.5)`

<img src="/teaser.png" width="640px" class="mx-auto" />

---

# what this talk isn't

(a very good talk)

- not a talk about godot XR
- no headsets or trackers are involved

<!--
add an image
-->

---
layout: image-right

image: badcop.png
backgroundSize: 20em
---

# who am i?

not actually a cop

- sarah a.k.a. "badcop"
- godot user for 5 years
- mostly game jams
- twitch streamer (software and game dev)

---

# software and game dev on twitch

there are dozens of us!

- variety of programming and game development content
- fairly small category

<div  class="relative">
  <div v-click>
most streams looks like this:
<img src="/every_stream.png" class="absolute w-120" />
    </div>
<img v-click src="/arrow.svg" class="absolute w-80 ml-60 rotate--20" />
<span v-after class="absolute text-[#FA0101] font-[Comic_Sans_MS] ml-145 mt--20 text-6xl">kinda<br>boring</span>
</div>

---

# could it be more visually interesting?

<div class="relative flex justify-center mt-10">
  <img v-click src="/iron1.png" class="ml--10 absolute w-180" />
  <img v-click src="/iron2.png" class="absolute w-140 mt-5" />
  <img v-click src="/iron3.png" class="ml-10 absolute mt-15 w-180" />
</div>
<!--
move the not a video production expert

add another slide here with the iron man stuff
-->

---
layout: quote
---

# i don't know how to do that stuff...

---
layout: quote
---

<div class="flex flex-1 items-center justify-between">

# ...but i *am* a game developer

<img src="/thonk.png" class="w-60 items-end" />
</div>

<!--
maybe the solution is to stop thinking about streaming like video production, and start thinking about it like game development
-->

---
layout: cover
---

<SlidevVideo src="demo.mp4" autoplay loop autoreset='slide' />

---

<SlidevVideo src="trippy.mp4" autoplay autoreset='slide' />

---

# let's rewind

it's rewind time

## how do streamers stream?

<br>

- pretty much everyone uses [OBS Studio](https://obsproject.com/)
- it does everything - capture, rendering, encoding, streaming
- lots of community plugins to extend functionality
- also lots of software that integrates with it

<v-click>

- ❌ it doesn't really do 3D

</v-click>

<img src="/obs.png" class="absolute right-30 top-40 w-50" />

---

# this is where Godot comes in

we've been waiting

- easier to bring OBS features into Godot vs. bring 3D to OBS
- scripting in Godot feels more productive than in OBS
  - ❌ **lua scripting in OBS**: thin wrapper around C API
  - ❌ **controlling OBS via websockets**: managing external state hard
  - ✅ **using GDScript**: lovely
- bonus points: i'm already familiar with it

<img src="/godot.png" class="w-60 mt-10 mx-auto" />

---
---


# initial goal

the plan is simple

<div>

<v-after>1. capture my camera and desktop in Godot<br></v-after>
<v-click>2. create a 3D scene out of that somehow<br>
</v-click>
<v-click>3. render the final stream output in Godot<br>
</v-click>
<v-click>4. still use OBS for audio / encoding / streaming<br>
</v-click>

<v-click><br><br><br>5. it only needs to work on Windows (sorry)</v-click>

</div>

---

# step 1: camera capture

it's never that simple

## Several Options

1. ❌ use Godot's [CameraServer](https://docs.godotengine.org/en/stable/classes/class_cameraserver.html)
    - no Windows support yet

<br>

2. ❌ use [godot-cameraserver-extension](https://github.com/j20001970/godot-cameraserver-extension)
    - gdextension that extends `CameraServer`
    - still very new and early development

<br>

3. ✅ Capture the camera in OBS, share it via [spout-gd](https://github.com/you-win/spout-gd)
    - works, but kinda resource intensive
<v-click>
  <li>maybe i can improve it?</li>
</v-click>

<img src="/spout.png" class="absolute right-40 top-40 w-50" />

---

# GPU and CPU

friends, or enemies?

- spout allows multiple programs to share a texture on the GPU
- supports DX11 and OpenGL

<img src="/dream.png" class="w-160 mx-auto" />

---

# GPU and CPU

friends, or enemies?

- Forward+ renderer uses Vulkan (or DX12)
- because of this, `spout-gd` takes the more scenic route


<img src="/reality.png" class="w-160 mx-auto" />

---

# learning Vulkan

<img src="/vulkan.jpg" class="mx-auto w-150" />

---
layout: quote
---

# ... maybe it's fine for now

i'm not "giving up", just "moving it to the backlog"

<!--
sometimes it's ok to give up on those rabbithole tasks
-->

---

# segmentation

fancy word for "separate the background"

<div class="relative justify-center flex">
<img src="/think.png" class="w-160 absolute" />
<img v-click src="/background.png" class="w-160 absolute" />
<img v-click src="/green_screen.png" class="w-160 absolute" />
</div>

---
---

# segmentation

fancy word for "separate the background"

<div class="flex justify-center gap-5 mt-20">
<img src="/background.png" class="w-80 border-1" />
  <span class="text-9xl pt-4">+</span>
<img src="/keyed.png" class="w-80 border-1" />
  </div>

---

# ... it looks bad.

<img src="/gru.jpg" class="w-160 mx-auto" />

---
---

# why?

<div v-click.hide class="flex justify-between flex-row items-start">

  <div>

- real cameras are imperfect
- random noise in the image changes each frame
- physics n' stuff




</div>
<img src="/noise.png" class="w-80 ml-20" />

</div>

<br>
<div v-after class="mt--60 bigger">

## we can fix it!

```glsl
// generates noise
float random (vec2 st) {
    return fract(sin(dot(st.xy,
         vec2(12.9898,78.233)))*
        43758.5453123);
}

void fragment() {
  float tex = texture(camera, UV).rgb;
  float rand = mod(random(UV) + TIME * 2.0, 1.0);
  ALBEDO = tex + vec3(rand) * 0.004;
}
```
</div>

<!--
add some code highlight annotations mebe
-->

---

# step 2: make it 3D

it's usually easier to go the other way...

- machine learning? photogrammetry? magic?

<br>

<img src="/photogrammetry.jpg" class="w-150 mx-auto" />

<img v-click src="/big_x.svg" class="absolute w-200 top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/3" />
---

# step 2: make it 3D

it's usually easier to go the other way...

<div class="flex justify-center gap-5 mt-20">
<img src="/blender.svg" class="w-80" />
  <span class="text-9xl pt-18">+</span>
<img src="/tape_measure.png" class="w-80" />
  </div>

---

# step 2: make it 3D

it's usually easier to go the other way...

<img src="/lol_blender.png" class="w-160 mx-auto" />

---

# projection un-mapping

not a very exact science

- free open source tool called [fSpy](https://fspy.io/)

<br>

<img src="/fspy.jpg" class="w-130 mx-auto" />

---

# projection un-mapping

not a very exact science

<img src="/aligned.png" class="w-130 mx-auto" />

---

# re-projecting

make it look like before again

<div>

how do we apply the texture to the model?

</div>
<div class="bigger">

````md magic-move {lines: true}
```glsl {all|2}
void fragment() {
  vec4 color = texture(albedo_texture, UV);
  ALBEDO = color.rgb;
}
```

```glsl {2|all}
void fragment() {
  vec4 color = texture(albedo_texture, SCREEN_UV);
  ALBEDO = color.rgb;
}
```
````

  </div>

---

# re-projecting

make it look like before again


<SlidevVideo src="panning.mp4" autoplay loop class="absolute w-180 left-30 top-35"/>

---

# re-projecting

make it look like before again

<img src="/same.jpg" class="w-170 mx-auto" />

---

# depth of field blur

it just works!

<SlidevVideo src="dof.mp4" autoplay loop autoreset='slide' class="absolute w-180 left-30 top-35"/>

---
---

# step 3: window capture

<br>
<br>

- i wrote a [gdextension](https://github.com/cgsdev0/gd-capture-external)
- supports capturing windows by ID
- exposes the window as a `Texture`
- uses the `WindowsGraphicsCapture` API
- the code is bad, but it's available

<img src="/no_desc.png" class="absolute bottom-10" />
<img src="/gooder.png" class="absolute right-5 top-35 w-120" />

---

# transparency was a mistake

why can't everything just be opaque?

<div class="relative">
<img src="/blur_cancel.png" class="w-120 absolute" />
<img v-click src="/blur_cancel.png" class="mt-49 scale-[1.1] ml-100 w-100 h-50 absolute object-none object-[50%_35%] blur" />
<img v-after src="/blur_cancel.png" class="mt-49 scale-[1.1] ml-100 w-100 h-50 absolute object-none object-[50%_35%]" />
  </div>

---

# solution: two rendering passes

it only needs to run at 60 fps anyways

<img src="/two_pass.png" class="w-180 mx-auto" />


---

# i really want glowy intersections

no matter the cost

<div class="flex gap-20 justify-center">
<img src="/glow1.png" class="w-90" />
<img src="/glow2.png" class="w-90" />
</div>

---

# we simply use the depth texture

nothing will go wrong (lol)

- popularly used effect, available on [godotshaders.com](https://godotshaders.com/shader/shield-shader-with-intersection-highlight/)

<br>

<div class="flex gap-10 justify-center">
<img src="/shield.png" class="w-100" />
<img src="/depth.png" class="w-100" />
</div>

---
layout: quote
---

# we have a new problem

who could have predicted this

---

# solution: *three* rendering passes

it only needs to run at 30 fps anyways

<br>
<br>

- one more `SubViewport`
- only draws opaque geometry

<img src="/three_pass.png" class="absolute top-30 right-10" />

<br>
<br>
<br>
<br>
<v-click>

## one more tiny problem


<br>

- small quirk; `SubViewport` uses a `R8G8B8` texture
- if we only use one channel, we're downgrading from 32 bits -> 8 bits

<v-click>

- (that's bad)

</v-click>
</v-click>
---

# RE: solution: solution

last one, i promise

<div class="bigger">

we can use some math in our shader to pack a `float` to a `vec3`


```glsl
vec3 PackFloatInVec3(float afX) {
    vec3 vRet;
    afX *= 255.0;
    vRet.x = floor(afX);
    afX = (afX - vRet.x) * 255.0;
    vRet.y = floor(afX);
    vRet.z = afX - vRet.y;
    vRet.xy *= (1.0 / 255.0);
    return vRet;
}
```

</div>


---

# RE: solution: solution

last one, i promise

<div class="bigger">

unpack it on the other side:

```glsl
float UnpackVec3ToFloat(vec3 avVal) {
    return dot(avVal, vec3(1.0, 1.0 / 255.0, 1.0 / (255.0*255.0)));
}
```

</div>

---

# RE: solution: solution

last one, i promise

<div class="flex justify-center gap-5 items-center mt-20">
<img src="/depth.png" class="w-90 " />
<span class="text-6xl">&rarr;</span>
<img src="/very_deep.png" class="w-90 " />
</div>

---

# what's next

follow me on twitch to find out (jk)
- physics objects
- more integrations with twitch chat / redeems
- tie some animations to hand tracking

<SlidevVideo src="hands.mp4" autoplay loop class="w-100 absolute top-40 right-15"/>

---
layout: image-left
image: love.png
backgroundSize: 40em
---

# final thoughts

special thanks to...
### code help
- [StaydMcmuffin](https://www.twitch.tv/staydmcmuffin)
- [LainVT](https://www.twitch.tv/lainvt)

<br>

### streamers who inspired me
- [CR4ZYK1TTY](https://www.twitch.tv/staydmcmuffin)
- [JDDoesDev](https://www.twitch.tv/jddoesdev)
- [Venorrak](https://www.twitch.tv/venorrak)
- [LCOLONQ](https://www.twitch.tv/lcolonq)
- [mdxcai](https://www.twitch.tv/mdxcai)
