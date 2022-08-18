# 06-fullscreen-and-resizing

## About
You don't need WebGL to fit the whole screen but for immersive experiences this is what you need to know:
- What a pixel ratio is
- How to resize to fit the application
- How HTML and CSS work with Three.js


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
## Sizing concepts
### Fitting the viewport

To fit your scene to the application viewport we use window.innerWidth and window.innerHeight
```
// Sizes
const sizes = {
    width: window.innerWidth,
    height: window.innerHeight
}
```

Most browsers have default stylings like more significant tiles, underlined links, space between paragraphs, and paddings on the page. Some of the ways to fix this is by altering the CSS. We could remove any type of margin or padding by using a wild card.
```
*
{
    margin: 0;
    padding: 0;
}
```
We can call the canvas element on the top left. Some browsers have a blue outline that we can get rid of.
```
.webgl
{
    position: fixed;
    top: 0;
    left: 0;
    outline: none;
}
```
There is a scrolling that occurs at the bottom of the page that breaks immersion with a white scrolling area
```
html,
body
{
    overflow: hidden;
}
```

### Resize events

To resize we use a native javascript event listener, in it we change the height/width and update the camera aspect ratio, then the renderer fills the new space.
```
window.addEventListener('resize', () =>
{
    // Update sizes
    sizes.width = window.innerWidth
    sizes.height = window.innerHeight

    // Update camera
    camera.aspect = sizes.width / sizes.height
    camera.updateProjectionMatrix()

    // Update renderer
    renderer.setSize(sizes.width, sizes.height)
})
```
### Pixel ratio

We really don't need pixel ratios higher than 2. Anything past could cause a "step-like" blur. to fix this we can set the pixel ratio. we can add this after the renderer is instantiated as well as in the resize event listener.
```
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
```

### Full screen
to get full screen we need a way to toggle it, this can be a button or any sort of UI. An easy way, building upon what we've learned is to use a native Javascript event listener for double clicking. We have to see if we are in full screen or not and we have to do this for chrome and Safari. If you don't want to do it for safari then you can leave out the webkit versions.

```
window.addEventListener('dblclick', () =>
{
    const fullscreenElement = document.fullscreenElement || document.webkitFullscreenElement

    if(!fullscreenElement)
    {
        if(canvas.requestFullscreen)
        {
            canvas.requestFullscreen()
        }
        else if(canvas.webkitRequestFullscreen)
        {
            canvas.webkitRequestFullscreen()
        }
    }
    else
    {
        if(document.exitFullscreen)
        {
            document.exitFullscreen()
        }
        else if(document.webkitExitFullscreen)
        {
            document.webkitExitFullscreen()
        }
    }
})
```