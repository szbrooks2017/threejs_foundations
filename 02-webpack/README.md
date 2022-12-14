# 02-webpack

## About
Loading three.js manually is easy, but has limitations as there are more classes than can be included in a file. A better way of loading all the dependencies is with a bundler. 

In this repository we will learn:
- How to set up Node.js
- What bundlers are
- How to launch a local server

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

## Bundlers
A bundler is a tool which sends assets like JS/CSS/HTML/imgs/ into a new JS output file ready for the web known as the *bundle file*.

## Webpack
[Webpack](https://webpack.js.org/) is currently the most popular bundler. 

## Node.js
Node.js is a runtime environment built on Chrome's V8 JavaScript Engine. Designed for scalable network applications. In the project folder use the command `npm install` to install dependencies like Three.JS, using npm. `npm` is the package manager that comes with Node.js.

`npm run dev` can launch a local server, alternatively you can click `Go Live` in VScode. If npm run dev doesn't automatically work, enter `http://localhost:8080` in your browser. To stop a server `CTRL + C`.

`npm build` builds a folder containing a package.json file in its root. This folder can be added to your website.