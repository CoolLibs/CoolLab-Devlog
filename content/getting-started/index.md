---
title: "Getting Started"
toc: true
---

If you want to take part in the discussion, join us on Discord ! https://discord.gg/JuNbK5Squb

Below you will find useful information to start working on the project.

## Cloning

Since we use submodules, you need to clone them too. The easiest way is to use the command :
```
git clone --recurse-submodules https://github.com/CoolLibs/CoolLab
```

## Building

## Git Submodules

Cool is highly based on the concept of submodule. Each small Cool library is included in the main project as a submodule. It allows us to keep all the repositories separated and share them across projects.

To add a new submodule to the project :

{{< figureCupper
img="gitkraken-add-submodule.png" 
caption="Add the repo as a submodule. Make sure to put it in the Cool folder (in the \"Name/Path\" field)"
command="Resize" 
options="700x" >}}

{{< figureCupper
img="cmake-add-submodule.png" 
caption="Declare the submodule in the CMakeLists.txt" 
command="Resize" 
options="700x" >}}

## Work on a branch !

## Commit message style