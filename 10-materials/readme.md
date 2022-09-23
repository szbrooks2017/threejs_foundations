# 10-materials

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

### Material update
since the 125th version of Three.js buffer geometries have been replaced with non buffer geometries so instead of PlaneBufferGeometry use `PlaneGeometry`.

