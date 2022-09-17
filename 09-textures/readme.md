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