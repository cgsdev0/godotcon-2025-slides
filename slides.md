---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Using Godot for mixed-reality livestreaming
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
# transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# open graph
# seoMeta:
#  ogImage: https://cover.sli.dev
---

# Using Godot for mixed-reality livestreaming

(it's not as scary as it sounds)


<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
---

# what does that mean

- mixed reality is just when 3d but also camera
- exploratory project over past 2 months

- show a teaser image
---
---

# what this talk isn't

- not a talk about godot XR
- no headsets or trackers are involved

---
---

# who am i

- sarah a.k.a. "badcop"
- godot user for 5 years
- mostly game jams
- twitch streamer (software and game dev)

---
---

# coding streams are kinda boring

- most streams looks like this:

if coding is boring, why is it the visual focus of the stream

---
---

# what i've been making

- show some of the results

---
---

# why godot

- traditional streaming tools confused my programmer brain
- what's easier? bring 3D engine to OBS, or bring OBS to 3D engine?

---
---


# goal

- do all of the capture and rendering in godot
- still use OBS for streaming

---
---

# segmentation

fancy word for "separate the background"

## background removal

- don't need a green screen
- actual live background

## green screen

- cleaner edges
- less resource hungry

---
---

# just add noise

- makes a static image look like a video feed

---
---

# modeling the environment

- simple blockout using blender
- tape measure

---
---

# projection mapping

- there was some tool i forgot tho

---
---

# 2D -> 3D -> 2D

---
---

# depth of field blur

- it just works!

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

# camera capture

using spout-gd for now

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

# Final Thoughts

Special thanks to...
### Code help
- StaydMcmuffin
- LainVT

<br>

### Inspiring streamers
- CR4ZYK1TTY
- JDDoesDev
- Venorrak
- LCOLONQ
