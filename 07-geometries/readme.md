# 07-Geometries

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
## Geometry Concepts

### Geometry for Three.js
In three.js geometries are composed of vertices and faces that creates a mesh. For particles each vertice can respond to a particle. Each vertex can have different data like position, UV, normal, size etc.

### Built in Geometries
[BoxGeometry](https://threejs.org/docs/#api/en/geometries/BoxGeometry) - class for a rectangular cuboid.

[BufferGeometry](https://threejs.org/docs/#api/en/core/BufferGeometry) - a mesh representative.

[PlaneGeometry](https://threejs.org/docs/#api/en/geometries/PlaneGeometry) - generates planes made of two triangles

[CircleGeometry](https://threejs.org/docs/#api/en/geometries/CircleGeometry) - creates a circle

[ConeGeometry](https://threejs.org/docs/#api/en/geometries/ConeGeometry)- create a cone

[CylinderGeometry](https://threejs.org/docs/#api/en/geometries/CylinderGeometry) - create a cylinder

[RingGeometry](https://threejs.org/docs/#api/en/geometries/RingGeometry) - create a flat sided ring

[TorusGeometry](https://threejs.org/docs/#api/en/geometries/TorusGeometry) - create a torus ring

[TorusKnotGeometry](https://threejs.org/docs/#api/en/geometries/TorusKnotGeometry) - create a torus knot to test light

[DodecahedronGeometry](https://threejs.org/docs/#api/en/geometries/DodecahedronGeometry) - it's a dodecahedron

[OctahedronGeometry](https://threejs.org/docs/#api/en/geometries/OctahedronGeometry) - it's like an 8 sided dice

[TetrahedronGeometry](https://threejs.org/docs/#api/en/geometries/TetrahedronGeometry) - it's like a 4 sided dice

[IcosahedronGeometry](https://threejs.org/docs/#api/en/geometries/IcosahedronGeometry) - it's an icosahedron

[SphereGeometry](https://threejs.org/docs/#api/en/geometries/SphereGeometry) - it's a sphere

[ShapeGeometry](https://threejs.org/docs/#api/en/geometries/ShapeGeometry) - create a custom shape

[TubeGeometry](https://threejs.org/docs/#api/en/geometries/TubeGeometry) - creates a tube

[ExtrudeGeometry](https://threejs.org/docs/#api/en/geometries/ExtrudeGeometry) - it'slike a cube but with dull edges.

[LatheGeometry](https://threejs.org/docs/#api/en/geometries/LatheGeometry) - create  a line and it duplicates it around.

[TextGeometry](https://threejs.org/docs/?q=textge#examples/en/geometries/TextGeometry) - create 3d text

### Box Geometry constructor

BoxGeometry(width : Float, height : Float, depth : Float, widthSegments : Integer, heightSegments : Integer, depthSegments : Integer)

width — Width; that is, the length of the edges parallel to the X axis. Optional; defaults to 1.
height — Height; that is, the length of the edges parallel to the Y axis. Optional; defaults to 1.
depth — Depth; that is, the length of the edges parallel to the Z axis. Optional; defaults to 1.
widthSegments — Number of segmented rectangular faces along the width of the sides. Optional; defaults to 1.
heightSegments — Number of segmented rectangular faces along the height of the sides. Optional; defaults to 1.
depthSegments — Number of segmented rectangular faces along the depth of the sides. Optional; defaults to 1.

If you set the subdivision to 2 you'll end up with 8 triangles.
```
const geometry = new THREE.BoxGeometry( 1, 1, 1 );
const material = new THREE.MeshBasicMaterial( {color: 0x00ff00} );
const cube = new THREE.Mesh( geometry, material );
scene.add( cube );
```

### Buffer Geometry 

Before creating a buffer geometry we have to understand how to store buffer geometry data. We are going to use a `Float32Array`- typed array, can store only floats, fixed length, easier to handle for the computer.

```
const positionsArray = new Float32Array(9)

// First vertice
positionsArray[0] = 0
positionsArray[1] = 0
positionsArray[2] = 0

// Second vertice
positionsArray[3] = 0
positionsArray[4] = 1
positionsArray[5] = 0

// Third vertice
positionsArray[6] = 1
positionsArray[7] = 0
positionsArray[8] = 0
```
another way of instantiating a Float32Array is 
```
const positionsArray = new Float32Array([
    0, 0, 0, // First vertex
    0, 1, 0, // Second vertex
    1, 0, 0  // Third vertex
])
```

Before you can send this array to the `BufferGeometry` we have to send it to the `BufferAttribute` The first parameter corresponds to your typed array and the second parameter corresponds to how much values make one vertex attribute

```
const positionsAttribute = new THREE.BufferAttribute(positionsArray, 3)
```
we have to go 3 by 3 because a vertex position is composed of 3 values (x, y and z).

Then we can add this attribute to our `BufferGeometry` using the `setAttribute()` method. The first parameter is the name of this attribute and the second parameter is the value:
```
geometry.setAttribute('position', positionsAttribute)
```
'position' is the name because Three.js internal shaders will look for that value to position the vertices

We can also create a bunch of random triangles
```
// Create an empty BufferGeometry
const geometry = new THREE.BufferGeometry()

// Create 50 triangles (450 values)
const count = 50
const positionsArray = new Float32Array(count * 3 * 3)
for(let i = 0; i < count * 3 * 3; i++)
{
    positionsArray[i] = (Math.random() - 0.5) * 4
}

// Create the attribute and name it 'position'
const positionsAttribute = new THREE.BufferAttribute(positionsArray, 3)
geometry.setAttribute('position', positionsAttribute)
```
We need 50 triangles. Each triangle is composed of 3 vertices and each vertex is composed of 3 values (x, y, and z).