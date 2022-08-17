# 05-cameras

## Setup
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

## Camera Concepts

[Camera()](https://threejs.org/docs/#api/en/cameras/Camera) - Is an abstract camera class for three.js and not intended to be called directly. This creates a new Camera.

[ArrayCamera()](https://threejs.org/docs/#api/en/cameras/ArrayCamera) - can be used in order to efficiently render a scene with a predefined set of cameras. Important for VR scenes. 

[StereoCamera()](https://threejs.org/docs/#api/en/cameras/StereoCamera) - used to render scene through two cameras for basic VR like Google cardboard.

[CubeCamera()](https://threejs.org/docs/#api/en/cameras/CubeCamera) - creates 6 renders, each one facing a different direction. Can render the surrounding objects like an environment map, reflection, refraction, or shadow maps.

[OrthographicCamera()](https://threejs.org/docs/#api/en/cameras/OrthographicCamera) - renders a scene without perspective. An object's size is constatn regardless of distance to the camera.

[PerspectiveCamera()](https://threejs.org/docs/#api/en/cameras/PerspectiveCamera) - this projection mode mimics human eyes to render 3D scenes. 

### Perspective Camera
The constructor for the Perspective Camera requires the following.

PerspectiveCamera( fov : Number, aspect : Number, near : Number, far : Number )

fov — Camera frustum *vertical* field of view in degrees.
aspect ratio — the width of the render divided by the height
near — Near clipping plane of the frustum view
far — Far clipping plane of the frustum view

```
const camera = new THREE.PerspectiveCamera( 45, width / height, 1, 1000 );
scene.add( camera );
```

**z-fighting** is when objects clip by being too close, extreeme near and far clipping plane values can cause this.

### OrthographicCamera
The constructor for the Otrthographic Camera requires the following.

OrthographicCamera( left : Number, right : Number, top : Number, bottom : Number, near : Number, far : Number )

left — Camera frustum left plane.
right — Camera frustum right plane.
top — Camera frustum top plane.
bottom — Camera frustum bottom plane.
near — Camera frustum near plane.
far — Camera frustum far plane.

```
const camera = new THREE.OrthographicCamera( width / - 2, width / 2, height / 2, height / - 2, 1, 1000 );
scene.add( camera );
```

### Custom Controls & Built in
to have better control of working with 3D space we can create custom controls

#### Custom window controls
We can use an event listner that moves the camera when we move our mouse. ClientX provides a horizontal coordinate within the application's viewport. We can make it to where the values don't go over 1 if we - 0.5

```
const cursor = {
    x:0,
    y:0
}

window.addEventListener('mousemove',(event) => 
{
    cursor.x = event.clientX / sizes.width - 0.5
    cursor.y = - (event.clientY / sizes.height - 0.5)
    console.log(cursor.y)
})
```

The camera's position gets updated, to achieve circular rotation we use sin and cos.

```
camera.position.x = Math.sin(cursor.x * Math.PI * 2) * 3
camera.position.z = Math.cos(cursor.x * Math.PI * 2) * 3
camera.position.y = cursor.y * 5
camera.lookAt(mesh.position)
```

### Built in Controls
[Fly Controls](https://threejs.org/docs/#examples/en/controls/FlyControls) - enables navigation similar to fly modes.

[First Person](https://threejs.org/docs/#examples/en/controls/FirstPersonControls) - like a bird's eye view of flying in the.

[PointerLockControl](https://threejs.org/docs/#examples/en/controls/PointerLockControls) - This API hides the cursor and keeps it centered, and keeps sending the movements in the mousemove event callback.

[OrbitControls](https://threejs.org/docs/#examples/en/controls/OrbitControls) - is similar to the custom controls we made. you can rotate around a point with the left mouse, translate with teh right mouse, and zoom with the wheel.

[TrackballControls](https://threejs.org/docs/#examples/en/controls/TrackballControls) is like orbit contorls but with no limit to vertical angle. you keep rotating and do spins with the camera even if the scene is upside down.

[TransformControls](https://threejs.org/docs/#examples/en/controls/TransformControls) - has nothing to do with the camera, you can use it to ad a gizmo to an object to move that object.

[Dragcontrols](https://threejs.org/docs/#examples/en/controls/DragControls) - like transform control, drag controls is used to move objects on a plane facing the camera by dragging and dropping.

### Orbit Controls implemented
we're going to use Orbit controls for our projects so to do this we need to do the following.

Instantiate Orbitcontrols
```
// Controls
const controls = new OrbitControls(camera, canvas)
controls.enableDamping = true
```
The function call takes in the camera and the dom element to store mouse queries.

Some Orbit Control features requires updating for each frame so in our animation loop add
```
controls.update()
```