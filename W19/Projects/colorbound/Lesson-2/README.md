# Meet-Up #2 Agenda:

**Objective**: Simplify asset loading, get an animated sprite on the screen and learn how to use tiled + display/collide with a tilemap

Please sign up for the general slack at https://uwcoffeencode.slack.com if you haven't already. Make sure you
join the game-dev-2-colorbound channel.

## 1. Tools
* Tiled map editor (https://www.mapeditor.org)

## 2. Simplifying Asset Loading
Right now, working with images is a pain. We do the following every time we want to load an image:

```js
let someImage = null;

let image = new Image();

image.addEventListener("load", function() {
    someImage = image;
});

image.src = "assets/heart.png";
```

Later, we check if the `someImage` variable before using it so our browser doesn't complain.

We could alternatively do this:

```js
let someImage = new Image();
someImage.src = "heart.png";

// Somewhere else
if(!someImage.complete) {
    return;
}
```

But this is still annoying because we have to do this check before using images anywhere.
Often, we'd like our assets (images or any similar resource) to be loaded by the time we run the code that uses them.

How can we make sure this is the case?
Well, what if we simply do nothing in our game loop unless all images are loaded?

This will solve the problem of having to perform the checks in our code since none of our code
would be executed unless all resources are loaded.

We can keep track of how many resources have yet to be loaded and skip our game loop code if there's still some waiting.

```js
// preload.js
let loadingImagesCount = 0;

function loadImage(filename) {
    let image = new Image();

    image.addEventListener("load", function() {
        loadingImagesCount -= 1;
    });    

    image.src = filename;
    loadingImagesCount += 1;

    return image;
}

function areAllAssetsLoaded() {
    return loadingImagesCount == 0;
}

// In loop.js
function loop() {
    if(areAllAssetsLoaded()) {
        processInput();
        update();
        draw();
    }

    requestAnimationFrame(loop);
}
```

Now, our code which loads images can be replaced with the following:

```js
let image = loadImage("heart.png");
```

And we can simply draw this image in our `draw` function because we can rest assured that
the draw function will never be called when images are still being loaded.
