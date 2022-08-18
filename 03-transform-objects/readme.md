# 03-transform-objects

## About
Exploring matrices and transforming objects. In this repository we will learn:
- What a Vector3 is
- What an Object3D is
- How to transform, scale, and move objects
- How to make an object look at another.

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

## Vocabulary

- [Vector3](https://threejs.org/docs/#api/en/math/Vector3) - represents a point in 3D space, labeled x, y, z. 

- [Mesh](https://threejs.org/docs/#api/en/objects/Mesh) - is a class representing a polygon mesh object base.

- [PerspectiveCamera](https://threejs.org/docs/#api/en/cameras/PerspectiveCamera) - is a camera designed to mimic the way human eyes sees, it renders 3D space

- [Object3D](https://threejs.org/docs/#api/en/core/Object3D) -  is the base class in three.js and provides a set or properties for manipulating 3D space.

- [AxesHelper](https://threejs.org/docs/#api/en/helpers/AxesHelper) - is a visualization of x (red), y (green), and z (blue).

- [Euler](https://threejs.org/docs/index.html#api/en/math/Euler) - describes a rotational transformation by rotating an object on its various axes.

- [Quarternion](https://threejs.org/docs/#api/en/math/Quaternion) - represents rotations.

- [Group](https://threejs.org/docs/#api/en/objects/Group) - almost identitcal to Object3D,makes working with groups of objects clearer.

## Transforming objects

### Moving postion
Moving objects can be done with `mesh.position.set(x, y , z)`

you can get the length of a vector with `console.log(mesh.position.length())`

you can get the distance from another Vector3 `console.log(mesh.position.distanceTo(camera.position))`

you can normalize the value meaning that you will reduce the length of the vector to 1 unit but preserve its direction `meaning that you will reduce the length of the vector to 1 unit but preserve its direction`

### Axes Helper
The AxesHelper will display 3 lines corresponding to the x, y and z axes, each one starting at the center of the scene and going in the corresponding direction.

To instantiate an AxesHelper
```
/**
 * Axes Helper
 */
const axesHelper = new THREE.AxesHelper(2)
scene.add(axesHelper)
```

### Scale
Scale is also a Vector3, if you put 0.5f then it will be half of it's original size, 2 would be double etc.

```
mesh.scale.x = 2
mesh.scale.y = 0.25
mesh.scale.z = 0.5 
```

### Rotating objects
Rotation is a **euler**, expressed in radians. to achieve half a rotation you times it by PI

```
mesh.rotation.x = Math.PI * 0.25
mesh.rotation.y = Math.PI * 0.25
```
Euler's howerver can cause issues by the order you rotate 'yxz' etc.

**Quarternion** expresses rotation in a more mathematical way that solves the order problem, it rotates everything at the same time.

## Look at this
Object3D instances have a method called lookAt() that lets you ask an object to look at something. the object will automatically rotate its -z axis toward teh target you provided.

`camera.lookAt(new THREE.Vector3(0, - 1, 0))`