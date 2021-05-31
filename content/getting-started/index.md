---
title: "Getting Started"
toc: true
---

If you want to take part in the discussion, join us on Discord ! https://discord.gg/JuNbK5Squb

Here you will find useful information to start working on the project :

## Clone

Since we use Git submodules, you need to clone them alongside the project. The easiest way is to use the command :
```
git clone --recurse-submodules https://github.com/CoolLibs/CoolLab
```

## Build

## Work on a branch

**Never commit directly on the *main* branch !** This is to avoid having to resolve merge conflicts on every commit while many people work on different areas. It is simpler that we each work on a branch, and only merge once in a while.

When you start working on a feature, create a dedicated branch and work there.

Once the feature is finished (or advanced enough that it would be interesting to merge) :
- merge *main* into your branch and resolve any conflict that might arise
- submit a pull request and wait for the peer review

## How to : Add a Submodule

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

## How to : Write a Cool Submodule

## When to : Write a Cool Submodule

## Commit Guidelines

### Make a lot of a small commits

As soon as you have made meaningful progress and the code compiles, make a commit !

Try to avoid long lists of *unrelated* changes in a single commit.

### Message style

Be explicit. Don't strip words from your sentence.

Specify which class / method / file is modified by the commit, inside [ ].

Example commit message :
```
[NodeEditor] Generate sceneSDF from the nodes
```


## Coding Guidelines