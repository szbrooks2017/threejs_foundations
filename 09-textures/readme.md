# TTextures

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

## What are textures?
Textures is what covers the surface of the geometries for three.js.

**Color(albedo)** - The albedo texture applies pixels to geometries in the most basic form.

**Alpha** - this texture is a grayscale image where white will be visible and black won't.

**Height** - the height texture is a grayscale image that will move the vertices to create some relief. You'll need to add subdivision if you want to see it.

**Normal** - the normal texture will add small details, it won't move the verticies but it will lure the light into thinking that the face is oriented differently. Normal textures are useful to add details with good performance because you don't need to subdivide geometry.

**Ambient Occlusion** - the ambient occlusion texture is a grayscale image that will fake shadow in the surface's crevices while it is not physically accurate it helps create constrast.

**Metalness** - is a grayscale image that will specify which part is metallic(white) and non-metallic(black) to create reflection.

**Roughness** - is a grayscale image that comes with metalness and that will specify which part is rough(white) and which part is smooth(black). this information will help to dissipate the light. a carpet for example, is rugged and won't see reflection while water is smooth and would have light reflecting.

**PBR** - textures, follow Physically Based Rendering principles. [Basic theory of PBR](https://marmoset.co/posts/basic-theory-of-physically-based-rendering/) [indepth PBR](https://marmoset.co/posts/physically-based-rendering-and-you-can-too/).

## Loading textures

To load a texture you insert via Webpack two ways, you can put the image texture in the `/src/` foldre and import it like a normal Javascript dependency, or you can put the image in the `/static/` folder and access it by adding the path of the image to the URL.

**/src/**
```
import imageSource from './image.png'

console.log(imageSource)
```

**/static/**
```
const imageSource = '/image.png'

console.log(imageSource)
```

with Webpack you can ommit `/static` from the URL path, if you use other types of bundler the static approach might look different.

### Loading textures with native JS
with native JS you need an `Image` instance, listen to the `load` event and then change its `src` propertery to load the image.
```
const image = new Image()
const texture = new THREE.Texture(image)
image.addEventListener('load', () =>
{
    texture.needsUpdate = true
})
image.src = '/textures/door/color.jpg'
```

Then we update the material for our geometry
```
const material = new THREE.MeshBasicMaterial({ map: texture })
```

### Loading textures with TextureLoader
using `TextureLoader` is a more straightforward way of loading textures, and there are a whole set of resources and properties to call.

```
const textureLoader = new THREE.TextureLoader()
const texture = textureLoader.load('/textures/door/color.jpg')
```

any other textures can be loaded with this textureloader. 

```
const colorTexture = textureLoader.load('/textures/door/color.jpg')
const alphaTexture = textureLoader.load('/textures/door/alpha.jpg')
const heightTexture = textureLoader.load('/textures/door/height.jpg')
```

If you want to know the status of a texture you can with `load`, `progress`, and `error`.

If you have a bunch of textures then you can utilize a `LoadingManager` which has functions that utilize the previous properties.

```
const loadingManager = new THREE.LoadingManager()
loadingManager.onStart = () =>
{
    console.log('loading started')
}
loadingManager.onLoad = () =>
{
    console.log('loading finished')
}
loadingManager.onProgress = () =>
{
    console.log('loading progressing')
}
loadingManager.onError = () =>
{
    console.log('loading error')
}

const textureLoader = new THREE.TextureLoader(loadingManager)
```

## UV Unwrapping
You can imagine unwrapping like a box transforming from 2D to 3D. you can pull the UV 2D coordiantes with the `attributes.uv` properties.
```
console.log(geometry.attributes.uv)
```

## Transforming textures
you can tranform textures that apply to geometries.

**Repeat**
is a Vector 2 that repeats `colorTexture.repeat.x` then you'll need to update the wrapS and wrapT properties for it to repeat and not just be stretched.

```
colorTexture.wrapS = THREE.RepeatWrapping
colorTexture.wrapT = THREE.RepeatWrapping
```

**Offset**
you can use the offset property which is a Vector2 `colorTexture.offset.x = 0.5`

**Rotation**
rotation is a number corresponding to the angle in radians. `colorTexture.rotation = Math.PI * 0.25` Math.PI is half a circle, for a full circle you multiply times 2. the center of rotation can be changed by calling `colorTexture.center.x = 0.5`

**Filtering and Mipmapping**
Mipmapping is a technique that consists of creating half a smaller version of a texture again and again until you get a 1 x 1 texture. The GPU chooses the most appropriate version.Three.js handles this and you can choose teh filter alorithm to use.

**Minification Filter** 
happens when the pixels of the texture are smaller than the pixels of the render. The texture is too big for the surface it covers. You can change the minification filter with `minFilter` property. The default is `THREE.LinearMipmapLinearFilter`. Some others are
- THREE.NearestFilter
- THREE.LinearFilter
- THREE.NearestMipmapNearestFilter
- THREE.NearestMipmapLinearFilter
- THREE.LinearMipmapNearestFilter
- THREE.LinearMipmapLinearFilter

`colorTexture.minFilter = THREE.NearestFilter` for example.

**Magnification Filter**
The magnification filter works like the minification filter but the pixels are bigger than the render's pixels. The texture is too small for the surface it covers. You can change this with `magFilter` property. The default is `THREE.LinearFilter`. Some others are 
- THREE.NearestFilter
- THREE.LinearFilter

`colorTexture.magFilter = THREE.NearestFilter` and you'll see that the based image is presereved and you get a pixelated texture.

Only use the mipmaps for the `minFilter` property. If you are using `THREE.NearestFilter` you don't need mipmaps dn you can deactivate it. 
```
colorTexture.generateMipmaps = false
colorTexture.minFilter = THREE.NearestFilter
```

## Texture format and optimization
when you are making a texture think about the weight, the size(resolution), and the data.

**weight** you can use .jpg(lossy compression but lighter) or png(lossless compression but heavier), and if you really need to have secure weight then you can use [TinyPNG](https://tinypng.com/)

**size** each texture has to be stored in the GPU regardless of weight. mipmapping automatically increases teh number of pixels that has to be stored. to reduce the size of your image have your width and height be a power of 2 so that Three.js can divide the size of the texture by 2. for example **512x512**, **1024x1024**, or **512x2048**

**data** basically png has an alpha channel and the ability to confirm the RGB to prevent visual glitches.

## Where to find textures
- poliigon.com
- 3dtextures.me
- arroway-textures.ch

you can create your own with photoshop or [Substance Designer](https://www.adobe.com/products/substance3d-designer.html)