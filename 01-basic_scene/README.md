# 01-Basic Scene

## About
This is the first of several projects to explore Three.js, this repository includes:
- How to install three.js
- How to create a scene
- How to add objects to a scene
- What objects are made of
- How to create a camera

## Requirements for Three.js
- [three.js](https://threejs.org/) - click download.
- go to /build and copy three.min.js to project(later projects will use a package manager)

## Setting up a Three.js scene
[script.js](/01-basic_scene/script.js) There are four elements needed to create a scene: a scene container, objects, a camera, and a renderer.

### Scene Container
`const scene = new THREE.Scene()` creates a scene that will hold all the elements of a three.js project

### Objects
An object consists of a geometry, material, and mesh. In this case we are making a simple cube that calls `BoxGeometry()` that takes in a height, width, and depth. A `MeshBasicMaterial()` which takes a color. A mesh constructor `Mesh(geometry, material)` which takes the geometry and material we just created. Then we add it to the scene.

### Camera
There are different types of cameras but the one we will use most is `PerspectiveCamera()` which takes a **field of view** - the camera frustum vertical field of view, **aspect** - camera frustum aspect ratio, **near** - camera near clipping plane, **far** - camera far clipping plane.

### Renderer
Renders the scene from the camera point of view, drawn into a canvas. To create a render instance we need to call `WebGLRenderer()` which takes the size of the application. This can be whatever size or window.innerWidth / window.innerHeight

[index.html](/01-basic_scene/index.html) Holds the canvas that WebGL renders to. We pick up this DOM element in our js script with `document.querySelector('.webgl')`