# 04-animations

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

## Rendering Animation
the purpose of [requestAnimationFrame](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame) is to call the function provided on the next frame. Each new frame teh same function will be called.

### Animation Loop
We have an animation loop that calls the renderer each frame. Here we can add simple animation to objects, handle problems dealing with time and fps.

### Different time solutions
#### timeDeltaTime
creates a let variable set to [Date.now()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/now) which gets called in the animation loop.

deltaTime is the time in seconds between the last frame and the current frame.

```
//Time
const currentTime = Date.now()
const deltaTime = currentTime - time
time = currentTime
```

You can do simple animations by updating objects position/rotation

```
// Update Objects with delta time
mesh.position.x += 0.001 * deltaTime
mesh.rotation.y -= 0.001 * deltaTime
```

#### Clock
[Clock](https://threejs.org/docs/#api/en/core/Clock) is a three js object that keeps track of time. It uses performance.now otherwise the less accurate Date.now.

//Clock
const clock = new THREE.Clock()

You can update simple animations by updating objects position/rotation
```
mesh.position.y = Math.sin(elapsedTime)
mesh.position.x = Math.cos(elapsedTime)
```

#### gsap
[gsap](https://greensock.com/gsap/) is a professional grade animation for javascript for the web. It has it's own update/animation loop

```
gsap.to(mesh.position, { duration:1, delay: 1, x: 2})
gsap.to(mesh.position, { duration:1, delay: 2, x: 0})
```