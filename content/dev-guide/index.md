---
title: "Dev Guide"
toc: true
---

Here you will find useful information to start working on the project :

## Clone

Since we use Git submodules, you need to clone them alongside the project. The easiest way is to use the command :
```
git clone --recurse-submodules https://github.com/CoolLibs/CoolLab
```

## Build

Install [CMake](https://cmake.org/download/). If you already have it, make sure you have version 3.16 or later.

Then, I recommend [this VS Code extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools).

Finally you will need to setup the extension with a compiler. Here is [the tutorial](https://code.visualstudio.com/docs/cpp/cmake-linux). It is based on Linux but at the bottom of the page you will find the explanations to adapt it for [Windows](https://code.visualstudio.com/docs/cpp/config-msvc) and [Mac](https://code.visualstudio.com/docs/cpp/config-clang-mac).

## imgui.ini

The *imgui.ini* file stores the position and size of our ImGui windows. It is nice to have it on the repo so that anyone cloning it will get a nice UI layout from the get go.

But you might want to do 

```
git update-index --assume-unchanged imgui.ini
```

to ignore it from your commits (It does change every time you move a window in your app, so basically it would be present in every commit).

You should only commit it once in a while, when new windows are added for example.

## Logging

To log to the console, use
```cpp
Log::info("You can use a variable, or a string like this one, which can be templated with some curly braces like so : {} {}", variable1ThatWillGoInTheCurlyBraces, variable2);
Log::warn("same parameters");
Log::error("same parameters");
```
The difference is that *info* outputs green text, *warn* is yellow and *error* is red.
Also, *error* will trigger a breakpoint (you can use *error_without_breakpoint* instead if you don't want that behaviour).

Note that those logs will be removed in release builds.
If you want to display a message to the end user, use Log::ToUser instead of Log.

## OpenGL

### GLDebug

Always wrap your OpenGL calls in the *GLDebug(...)* macro. It will add debug checks even if your computer doesn't support modern OpenGL debugging.

```cpp
GLDebug(GLuint program_id = glCreateProgram());
GLDebug(glLinkProgram(program_id));
GLDebug(glValidateProgram(program_id));
```

### Modern Debugging (requires OpenGL 4.3 or later)

Modern debugging happens automatically.

You can ignore some warnings and control the look of the messages in the *App* module, under *internal/GLDebugCallback.h*.

## Write documentation

We use Doxygen-style documentation. I would suggest you install [this extension for VS Code](https://marketplace.visualstudio.com/items?itemName=cschlosser.doxdocgen)

Then you simply need to type */\*\** and press *enter* to generate the documenting comment for the class or method.

Try to be as descriptive as possible in your documentation : mention any hickups and subtleties, and give an example if the usage is not obvious.

```cpp
/**
 * @brief Returns the Color of the (x, y) pixel. No bound checking is done, so this will crash if x is not inside [0, width() - 1] or y is not inside [0, height() - 1]
 * 
 * @param x x coordinate of the pixel (0 is at the left of the image)
 * @param y y coordinate of the pixel (0 is at the bottom of the image)
 * @return The Color of the given pixel
 */
inline Color& color_at(unsigned int x, unsigned int y) { return _pixel_colors[x + y * _width]; }
```

## Write an article

It would be nice to have an article on this website for each module we write. The goal of those articles is to describe our thought process and the technical choices that we make (architecture, design pattern, optimization / simplicity of the API, . . .).

It is a great way of creating and sharing knowledge : these resources will surely prove useful to many one day, and forcing you to write down the choices you made should have you question whether they are really the best, and strive to improve your own design.

**To learn how to edit this website**, check it out [on GitHub](https://github.com/CoolLibs/CoolLab-Devlog/).

## Write debug checks

If there is some invariant that must be verified, add debug checks to make sure users of your code don't mess up !
You can use *assert* in the simpler cases, but sometimes you will need to add variables to keep track of some state. In that case, wrap the debug code in a 
```
#ifdef DEBUG
// . . .
#endif
```
block so that it doesn't impact release build performance.

An example would be to make sure an initialization function is called once, and only once :

```cpp
class MyClass {
public:
      void initialize() {
#ifdef DEBUG
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
#ifdef DEBUG
      bool _is_initialized = false;
#endif
};
```

## How to : Write a Cool module

Create a dedicated folder, and an "internal" folder inside it. In "internal" you will put your .cpp files, as well as the .h that are not part of the public API you want to expose.

Wrap your code in the Cool namespace

```cpp
namespace Cool {

class MyClass {
      // . . .
};

} // namespace Cool
```

## When to : Write a Cool module

Everything that might be reused across projects should be part of the Cool framework.

## Work on a branch

**Never commit directly on the *main* branch !** This is to avoid having to resolve merge conflicts on every commit while many people work on different areas. It is simpler that we each work on a branch, and only merge once in a while.

When you start working on a feature, create a dedicated branch and work there.

Once the feature is finished (or advanced enough that it would be interesting to merge) :
- merge *main* into your branch and resolve any conflict that might arise
- submit a pull request and wait for the peer review

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

There is a lot of great people out there that have gathered a big list of great ideas for your code, and they might prove useful to you one day.

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

I used to use camel case, and then started to learn Rust which forces you to use snake_case. And well, after a short period of adaptation I started really enjoying snake case because the separation between words is clearer, and therefore long names are easier to read.

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