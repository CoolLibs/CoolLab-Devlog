---
title: "Getting Started"
toc: true
---

If you want to take part in the discussion, [**join us on Discord**](https://discord.gg/JuNbK5Squb) !

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

## Write documentation

We use Doxygen-style documentation. I would suggest you install [this extension](https://marketplace.visualstudio.com/items?itemName=FinnGegenmantel.doxygenComments) for Visual Studio, or [this one]() for VS Code.

And good documentation always comes with examples. Here is an example of some good documentation : [p5.js](https://p5js.org/reference/#/p5/quad)

## Write an article

It would be nice to have an article on this website for each module we write. The goal of those articles is to describe our thought process and the technical choices that we make (architecture, design pattern, optimization / simplicity of the API, . . .).

It is a great way of creating and sharing knowledge : these resources will surely prove useful to many one day, and forcing you to write down the choices you made should have you question whether they are really the best, and strive to improve your own design.

**To learn how to edit this website**, check it out [on GitHub](https://github.com/CoolLibs/CoolLab-Devlog/).

## Write debug checks

If there is some invariant that must be verified, add debug checks to make sure users of your code don't mess up !
You can use *assert* in the simpler cases, but sometimes you will need to add variables to keep track of some state. In that case, wrap the debug code in a 
```
#ifndef NDEBUG
// . . .
#endif
```
block so that it doesn't impact release build performance.

An example would be to make sure an initialization function is called once, and only once :

```cpp
class MyClass {
public:
      void initialize() {
#ifndef NDEBUG
            assert(!_is_initialized);
            _is_initialized = true;
#endif
            // . . .
      }

      void use_my_class() {
            assert(_is_initialized);
            // . . .
      }

private:
#ifndef NDEBUG
      bool _is_initialized = false;
#endif
};
```

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

Wrap your code in the Cool namespace

```cpp
namespace Cool {

class MyClass {
      // . . .
};

} // namespace Cool
```

## When to : Write a Cool Submodule

## Commit Guidelines

### Make a lot of a small commits

As soon as you have made meaningful progress and the code compiles, make a commit !

Try to avoid long lists of *unrelated* changes in a single commit.

### Message style

Be explicit. Don't strip words from your sentence.

When appropriate, specify inside [ ] which class / method / file is modified by the commit.

Example commit message :
```
[NodeEditor] Generate sceneSDF from the nodes
```

## Coding Guidelines

### Naming

**Naming is important (and hard)**, so please be mindful when you choose a name. Be explicit, **don't be too afraid of long names**. And most importantly : make sure the name describes what the thing is, nothing more, nothing less.
Also, **don't hesitate to rename** as soon as you realize the name doesn't quite match what the thing actually is or does. (And by the way, *right click -> Rename* is an amazing feature).

*About naming* :
https://www.youtube.com/watch?v=FyCYva9DhsI&t=41m34s (watch until at least 51:30 if you want to laugh a lot)

*About comments* :
https://www.youtube.com/watch?v=FyCYva9DhsI&t=24m49s

(By the way, watch the whole conference it's great)

### Refer to the [C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)

There is a lot of great people out there that have gathered a big list of great ideas for your code, and they might prove usefull to you one day.

I would suggest you start by watching this amazing conference :

<iframe width="880" height="495" src="https://www.youtube.com/embed/XkDEzfpdcSg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Alignment

When you have multiple lines that are very similar, try to align the corresponding terms. This makes the similarities and differences between the lines way more obvious, and therefore the code structure clearer.

For example this :

```cpp
_angle_ground = _initial_angle_ground + delta.x;
_angle_up     = _initial_angle_up     + delta.y;
```

is, in my humble opinion, more readable than :

```cpp
_angle_ground = _initial_angle_ground + delta.x;
_angle_up = _initial_angle_up + delta.y;
```

### Coding style

Coding styles don't matter, and that's why we simply have to choose one and stick to it.

**There is no right answer** to where you should put your curly braces, or whether you shoud use camelCase or snake_case. If there was, all the developers of the world would have agreed on it years ago.

https://www.youtube.com/watch?v=XkDEzfpdcSg&t=3m15s

#### Snake Case

We could have chosen camelCase, but we chose snake_case.

I used to use camel case, and then started to learn Rust which forces you to use snake case. And well, after a short period of adaptation I started really enjoying snake case because the separation between words is clearer, and therefore long names are easier to read.

So here you are, I now use snake case.

#### Member variables

They are prefixed with an underscore like so :

```cpp
class MyClass {
public:
      MyClass() = default;
      MyClass(float my_member_variable);

private:
      float _my_member_variable = 0.f;
};
```