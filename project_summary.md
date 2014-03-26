# Yellow Tail
A magical cooperating drawing experience.

## Authors
- Jiaying Peng
- https://github.com/karenpeng
- http://karenlabs.com

## Description
Inspired by Golan Levin's Yellow Tail, I want to make xxxx. A huge display screen and everybody could use their own mobilephone to get involved in.

## Link to Prototype
NOTE: If your project lives online you can add one or more links here. Make sure you have a stable version of your project running before linking it.

[Yellow Tail](http://yellowtail.karenlabs.com "Yellow Tail")

## Example Code
NOTE: Wrap your code blocks or any code citation by using ``` like the example below.
```
function onFrame(event) {
  frameCount++;
  if (begin) {
    if (shake && worms.length > 0) {
      var mobileWorm = [];
      worms.forEach(function (w) {
        var myWorm = {
          p: w.path.toJSON()[1],
          m: w.mouseRelease,
          g: w.gap,
          d: w.dis
        };
        mobileWorm.push(myWorm);
        w.path.removeSegments();
        w = null;
      });
      socket.emit('mobileWorm', mobileWorm);
      worms = [];
    }

    for (var i = 0; i < worms.length; i++) {
      if (worms[i].check()) {
        worms.splice(i, 1);
      } else if (frameCount % 2 === 0) {
        worms[i].move();
      }
    }
  }
}
```
## Links to External Libraries
 NOTE: You can also use this space to link to external libraries or Github repositories you used on your project.

[Paper Js](http://paperjs.org/ "Paper Js")

## Images & Videos
NOTE: For additional images you can either use a relative link to an image on this repo or an absolute link to an externally hosted image.

![Example Image](project_images/cover.jpg?raw=true "Example Image")

http://www.youtube.com/watch?v=Lh_FMDDpVxA&list=UUsa7fbowwLi94D5M788uzPg
