# Debug UI

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

## Debug Options
There are several different ways to debug three.js. Here are the five most used, [dat.GUI](https://github.com/dataarts/dat.gui), [control-panel](https://github.com/freeman-lab/control-panel), [ControlKit](https://github.com/automat/controlkit.js), [Guify](https://github.com/colejd/guify), and [Oui](https://github.com/wearekuva/oui).

## Dat.GUI
Dat.GUI hasn't been updated for a long time so some vulnerabilities might show up, a replacement is [lil-gui](https://lil-gui.georgealways.com/). 

### Here is how to install lil-gui.

`npm install lil-gui --save-dev`

with either import statement

`import GUI from 'lil-gui';` or `import * as lil from 'lil-gui';`.

### Adding Controllers

```const gui = new GUI();
gui.add( document, 'title' );```

