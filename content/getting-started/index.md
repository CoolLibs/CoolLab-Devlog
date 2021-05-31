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

Coding styles don't matter, and that's why we simply have to choose one and stick to it.

**There is no right answer** to where you should put your curly braces, or whether you shoud use camelCase or snake_case. If there was, all the developers of the world would have agreed on it years ago.
So we just need to pick one, and move on.

https://www.youtube.com/watch?v=XkDEzfpdcSg&t=3m15s

### Naming

Naming is important (and hard), so please be mindful when you choose a name : be explicit, don't be too afraid of long names. And most importantly : make sure the name describes what the thing is, nothing more, nothing less.
Also, don't hesitate to rename, especially in the early days of the codebase, until we reach the right name. Everybody makes mistakes, but better fiw them ;) (And by the way, right click -> Rename is an amazing feature)

Create types and methods with explicit names, and rename them *as soon as* you realize the name doesn't quite match what the type actually is / what the method actually does.

About naming :
https://www.youtube.com/watch?v=FyCYva9DhsI&t=41m34s (watch until at least 51:30 if you want to laugh a lot)

About comments :
https://www.youtube.com/watch?v=FyCYva9DhsI&t=24m49s

(by the way, watch the whole conference it's great)

### Snake Case

We could have chosen camelCase, but we chose snake_case.

I used to use camel case

### Member variables

They are prefixed with an underscore like so :

```cpp
class MyClass {
public:
      MyClass() = default;
      MyClass(float my_member_variable);
      
private:
      float _my_member_variable = 0.f;
}
```