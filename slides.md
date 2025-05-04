---
# stuff
theme: default
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

(it's not as scary as it sounds)


<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
---

# what does that mean

`mix(real_camera, virtual_camera, 0.5)`

<div class="relative flex items-center justify-center">
  <img src="./public/Camera3D.svg" width="250px" class="object-contain" />
  <span class="text-9xl ml-5 mr-10">+</span>
  <img src="./public/sony.png" width="250px" class="mt-20 object-contain" />
</div>

---
layout: image
---

# what does that mean

`mix(real_camera, virtual_camera, 0.5)`

<img src="./public/teaser.png" width="640px" class="mx-auto" />

---
---

# what this talk isn't

(a very good talk)

- not a talk about godot XR
- no headsets or trackers are involved

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
---

# software and game dev on twitch

there are dozens of us!

- variety of programming and game development content
- fairly small category

<div  class="relative">
  <div v-click>
most streams looks like this:
<img src="./public/every_stream.png" class="absolute w-120" />
    </div>
<img v-click src="./public/arrow.svg" class="absolute w-80 ml-60 rotate--20" />
<span v-after class="absolute text-[#FA0101] font-[Comic_Sans_MS] ml-145 mt--20 text-6xl">kinda<br>boring</span>
</div>

<span v-click class="absolute ml-145 mt-20 text-2xl">i'm not a video production expert, oh well</span>
<!-- if coding is boring, why is it the visual focus of the stream -->

---
layout: quote
---

# ...but i *am* a game developer

---
---

# what it looks like now
visual effects fix everything

- show some of the results

---
---

# why godot?

*"but why male models?"*

- which is easier: bring 3D into OBS, or bring OBS features into Godot?
- scripting in Godot is a way nicer experience than OBS
- Godot is open source and easily extensible
- bonus points: i'm already familiar with it

---
---


# initial goal

the plan is simple

<v-after>1. capture my camera and desktop in Godot<br></v-after>
<v-click>2. create a 3D scene out of that somehow<br>
</v-click>
<v-click>3. render the final stream output in Godot<br>
</v-click>
<v-click>4. still use OBS for audio / encoding / streaming<br>
</v-click>

<v-click><br><br><br>5. it only needs to work on Windows (sorry)</v-click>

---

# step 1: camera capture

the unapologetic cheating begins

using spout-gd for now

talk about camera extension

add a slide for GPU->CPU->GPU explanation

spent some time trying to fix this, then realized "you know what, good enough"

---
---

# segmentation

fancy word for "separate the background"

## green screen

- cleaner edges
- less resource hungry

---
---

# it looks bad

- something looks... off

---
---

# just add noise

- makes a static image look like a video feed

---
---

# step 2: make it 3D

- simple blockout using blender
- tape measure

---
---

# projection un-mapping

not a very exact science

- there was some tool i forgot tho

---
---

# projection projection-ing

---
---

# depth of field blur

- it just works!

---
---

# step 3: window capture

- window capture in godot

---
---

# floating windows

- window capture in godot
- transparency sorting hell

---
---

# deep dive: packing floats

make some cool visuals

---
---

# hand tracking

lots of options (and they're all mediapipe)

GDMP vs. python vs. browser

---
---

# what's next

- physics objects
- more integrations with twitch chat / redeems
- doing more with hand tracking

---
---

# final thoughts

special thanks to...
### Code help
- StaydMcmuffin
- LainVT

<br>

### Inspiring streamers
- CR4ZYK1TTY
- JDDoesDev
- Venorrak
- LCOLONQ
