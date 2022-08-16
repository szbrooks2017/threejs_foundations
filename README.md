# threejs_foundations

## About
This repository is a survey of three.js concepts. Three.js sits on top of WebGl to render 2D and 3D content to the browser. WebGL is a web graphics API developed by the Kronos Group. We use three.js so we don't have to use a very low level GLSL--the language used by OpenGL for the GPU.

### Requirements for Three.js
#### Manual download
- [three.js](https://threejs.org/) - click download.
- go to /build and copy three.min.js to project

#### NPM download
- Use [Node.js](https://nodejs.org/en/) to manage packages and dependencies
- `npm install` to install dependencies

## Projects
[01-basic_scene](/01-basic_scene/) - Explains what is needed to create and render to the web browser a three.js scene with 3D objects.

[02-webpack](/02-webpack/) - Introduces web bundlers and installing three.js from Node.js.
 
[03-transform-objects](/03-transform-objects/) - Explores how to manipulate Vector3 objects.
