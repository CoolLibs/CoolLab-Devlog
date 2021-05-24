---
title: "Camera"
date: 2021-05-24T00:46:44+02:00
draft: false
author: jules
---

## Separate the data from the controller

![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")
![Alt text here](/src/images/is0.png)

```C++
int i = 0;
for (auto x = 0; x < 10; ++x) {
	i += x;
}
return x;
```

Especially since there can be different ways of controlling a camera (trackball, freefly, turntable, etc.)

## How separate should the view and the projection be ?

Although we tend to separate these into two matrices (and for good reasons), they should still stay together in a same class, because we need both to define a camera frustum. For example, to compute a ray passing through a given pixel, we need both the view and the projection.
```
Ray Camera::rayThroughPixel(const glm::vec2& positionInPixels) {
	glm::vec3 pos = position();
	glm::vec3 pixelPos = glm::unProject(glm::vec3(positionInPixels, 0.0f), viewMatrix(), projMatrix(), glm::vec4(0.0f, 0.0f, RenderState::Size().width(), RenderState::Size().height()));
	glm::vec3 dir = pixelPos - pos;
	return Ray(pos, dir);
}
```

## What's the point of clipping at a near and far plane ?

## Don't confuse projection and perspective