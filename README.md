# threejs_foundations

## About
This repository is a survey of three.js concepts. Three.js sits on top of WebGl to render 2D and 3D content to the browser. WebGL is a web graphics API developed by the Kronos Group. We use three.js so we don't have to use a very low level GLSL--the language used by OpenGL for the GPU.

### Requirements for Three.js
#### Manual download
- [three.js](https://threejs.org/) - click download.
- go to /build and copy three.min.js to project

#### NPM download
Download [Node.js](https://nodejs.org/en/download/).
Run this followed commands:

``` bash
# Install dependencies (only the first time)
npm install

# Run the local server at localhost:8080
npm run dev

# Build for production in the dist/ directory
npm run build
```

## Projects
[01-basic_scene](/01-basic_scene/) - Explains what is needed to create and render to the web browser a three.js scene with 3D objects.

[02-webpack](/02-webpack/) - Introduces web bundlers and installing three.js from Node.js.
 
[03-transform-objects](/03-transform-objects/) - Explores how to manipulate Vector3 objects.

[04-animation](/04-animations/) - Showcases different ways to run an animation loop or call a third party libary one.

[05-cameras](/05-cameras/) - Dives into the different type of cameras and use cases, as well as how to control them to build 3D scenes.

[06-fullscreen-and-resizing](/06-fullscreen-and-resizing/) - Explores the options of having your canvas resize to fit different viewports.

[07-geometries](/07-geometries/) - A look at built in geometries and how to create custom ones.

[08-debug-ui](/08-debug-ui/) - This is how we speed up production and debug problems.

[09-textures](/09-textures/) - What textures are and how to manipulate them.

[10-materials](/10-materials/) - How materials add color to geometries.