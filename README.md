

# The Polygons of Another World - Interactive Graphical Applications in R

This repository contains links and resources related to my talk at 
RStudioConf 2022.

<img src="image/polygons-of-another-world-realtime_talk-opt4.png" width = "50%" />



### Slides + Materials

* Slides for talk - **Coming Soon**
* [RStudio Conf Schedule](https://rstudioconf2022.sched.com/event/11ibb)
* Videos from presentation  (these won't play reliably on github, so please
      clone/checkout the repository and play locally)
    * [Drum machine](video/compose.mp4)
    * [5000 dinosaurs in {nara}](video/dino-5000.mp4)
    * [Another World - Intro](video/game-intro-trimmed.mp4)
    * [Another World - Jail](video/game-jail-trimmed.mp4)
* Original inspiration for this talk comes  [Fabien Sanglard's blog series](https://fabiensanglard.net/another_world_polygons/index.html) where 
they detail the struture of the game and how it was ported to different 
gaming platforms.

### Key packages

* [`{eventloop}`](https://github.com/coolbutuseless/eventloop) - provides 
  a friendly wrapper around the event-driven interactivity provided by
  R graphics devices.
    * See [online documentation](https://coolbutuseless.github.io/package/eventloop/index.html)
      to view rendered vignettes etc
* [`{nara}`](https://github.com/coolbutuseless/nara) - tools for
  fast manipulation of R's `nativeRaster` datastructure. 
    * See [online documentation](https://coolbutuseless.github.io/package/nara/index.html)
      to view rendered vignettes etc
  
  
### Games

* [`pacman`](https://github.com/coolbutuseless/pacman) - full code for a 
  playable game based on Pacman.
  <img src="image/pacman-game.gif" width="70%" />
* [`AnotherWorld`](https://github.com/coolbutuseless/anotherworld) - full code 
  AnotherWorld game written and playable in R.  **Coming Soon**
  
  
### `{eventloop}` Demos

|   |   |
|---|---|
| [Grid-based drawing <br/><img src="image/gallery/grid-based.png" width="89%" />](https://coolbutuseless.github.io/package/eventloop/articles/drawing-grid.html)   | [Line-based drawing <br/><img src="image/gallery/line-based.png" width="89%" />](https://coolbutuseless.github.io/package/eventloop/articles/drawing-lines.html)   | 
| [Streaming plot data <br/><img src="image/gallery/plot-stream.png" width="89%" />](https://coolbutuseless.github.io/package/eventloop/articles/stream-plotting.html) | [Game of Life <br/><img src="image/gallery/game-of-life.png" width="89%" />](https://coolbutuseless.github.io/package/eventloop/articles/game-of-life.html) |
| [Asteroids<br/><img src="image/gallery/asteroids.png" width="89%" />](https://coolbutuseless.github.io/package/eventloop/articles/game-asteroids.html) |  [Raycast 'Wolfenstein' 3d engine <br/><img src="image/gallery/raycast.png" width="89%"  />](https://coolbutuseless.github.io/package/eventloop/articles/game-raycaster.html) |  
| [Wordle <br/><img src="image/gallery/wordle.png" width="89%" />](https://coolbutuseless.github.io/package/eventloop/articles/game-wordle.html) | [Interactive Mystery Curves <br/><img src="image/gallery/mystery-curves.png" width="89%" />](https://coolbutuseless.github.io/package/eventloop/articles/verbose-example.html) | 
| [Verbose example <br/><img src="image/gallery/debug.png" width="89%" />](https://coolbutuseless.github.io/package/eventloop/articles/verbose-example.html) | [Particles <br/><img src="image/gallery/particles.png" width="89%" />](https://coolbutuseless.github.io/package/eventloop/articles/demo-particles.html) |
  
  
  
## Limitation - WindowsOS

The WindowsOS version of R does not currently have support for the `onIdle` callback and 
therefore does not support  event-driven interactive graphics as implemented 
in the `{eventloop}` package.

**If you are a windows developor capable of adding support for an `onIdle` callback
to R itself, please get in touch!**

## Limitation - Flickering Cursor

The cursor icon in an `{eventloop}` window will flicker because of some hard-coded
behaviour in R's double-buffered `x11()` graphics device.

`{eventloop}` makes use of the `x11()` graphics device with a double-buffered
backend based on Cairo  (`x11(type = 'dbcairo')`).

The double-buffering within the graphics device is coordinated through use
of `dev.hold()` and `dev.flush()` calls.

Whenever `dev.hold()` is called, the cursor will be set to the busy cursor
(usually a stopwatch on macOS), and when `dev.flush()` is called the 
cursor reverts to a normal pointer arrow.

Since `dev.hold()` and `dev.flush()` are called when drawing every single 
frame, the cursor will flicker between these two images.

The interim solution is to not have the cursor over the window when interacting
with the app.  This only really works when the app solely relies on keyboard
feedback (like this pacman game).

The more complicated solution will involve crafting a patch to R itself to
make the cursor change behaviour user-configurable rather than hard-coded.

**If you are are an R developer capable of crafting such a patch to R ,
please get in touch with me!**
