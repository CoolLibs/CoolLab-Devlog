---
title: "Our Roadmap"
date: 2021-05-24T23:29:21+02:00
author: jules
tags: []
toc: true
draft: false
---

## Layer system

How do we combine the outputs from our different system / from different instances of the same system.
Do we use a classic layer structure, or a graph ?

## Audio

Import audio files and play them along the image generation (ideal to produce audio clips). Retrieve data from the audio to drive the images (pitch, bpm, volume etc.)

We can search a lib in this list : https://awesomeopensource.com/projects/audio-library
I currently found https://github.com/mackron/miniaudio for audio playback
and https://www.kfrlib.com/newdocs/index.html or https://aubio.org/ for audio analysis.

## Parameter system

Data usable across the different systems.

## History / Multiple histories in parallel ?

## Simple compute shaders

## Project save

## Post-processing

## Color spaces ?

## Premultiplied alpha

## Improve timeline navigation / display

## Keybinds remapping (inspired from Django ?)

## Abstract GPU  API over OpenGL and Vulkan

## Node system

## Ray Marching

### Write many nodes

### Setup a material system

## Shaders

### Write libraries of shader functions

### Good include system / meta language on top of glsl

-> Look at shaderc (https://github.com/google/shaderc, https://www.youtube.com/watch?v=SXDlZRDjtXg) or naga (https://github.com/gfx-rs/naga)