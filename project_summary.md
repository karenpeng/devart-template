# Yellow Tail
A magical cooperating drawing experience.

## Authors
- Jiaying Peng
- https://github.com/karenpeng
- http://karenlabs.com

## Description
Inspired by Golan Levin's Yellowtail, I like the idea of drawing something then comes to life, also, I want to augment this magic moment in which the drawing transforms from static to dynamic.
What’s more, I'd like this drawing experience to be multi-player. Thus people could cooperate with each other coming up with drawing contents, strategies, etc.

Therefore I came down to the idea that using touch based devices for people to draw still strokes, and then desktop computers to display the vivid animation of their drawings. A shake from the mobile device triggers the transformation. And with web socket, communications between multiple clients is supported.

My ideal scenario of how this piece being played is that a huge display screen, or projector to a giant wall, in a public space invites people to participate in simply using their own smart phones or tablets.

## Link to Prototype
[Yellow Tail](http://yellowtail.karenlabs.com "Yellow Tail")

## Example Code
```
function onFrame(event) {
  frameCount++;
  if (begin) {
    if (shake && worms.length > 0) {
      var mobileWorm = [];
      worms.forEach(function (w) {
        var myWorm = {
          myPath        : w.path.toJSON()[1],
          myMouseRelease: w.mouseRelease,
          myGap         : w.gap,
          myDis         : w.dis
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
[Paper js](http://paperjs.org/ "Paper js")

## Images & Videos
http://www.youtube.com/watch?v=Lh_FMDDpVxA&list=UUsa7fbowwLi94D5M788uzPg
