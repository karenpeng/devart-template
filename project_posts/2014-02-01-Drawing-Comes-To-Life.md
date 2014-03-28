My original inspiration is Golan Levin’s <a href="http://www.flong.com/projects/yellowtail/">Yellowtail</a>, what I want to do is to emphasize the magic moment of drawing something that could become real.

I spend quite some time staring at the original piece, and going through the api of the framework I use: paperjs.

First, I realize that how I draw line with thickness is this:
![Points](../project_images/points.jpg?raw=true "Points")

Ths code is like this:
```
function onMouseDown(event) {
  path = new Path();
  path.fillColor = new Color({ hue: Math.random() * 360, saturation: 1, brightness: 1 });
  path.add(event.point);
}

function onMouseDrag(event) {
  var step = event.delta / 2;
  step.angle += 90;

  var top = event.middlePoint + step;
  var bottom = event.middlePoint - step;

  path.add(top);
  path.insert(0, bottom);
  path.smooth();
}

function onMouseUp(event) {
  path.add(event.point);
  path.closed = true;
  path.smooth();
}

```

Then, from the observation of Golan’s yellowtail,  I come down to the algorithm:
![Crawl](../project_images/crawl.jpg?raw=true "Crawl")
How it moves is simply repeating this procedure over and over again.

The code:
```
var newTop = this.path.segments[this.path.segments.length / 2 - 2].point +
  this.dis;
var newBottom = this.path.segments[this.path.segments.length / 2].point +
  this.dis;

this.path.removeSegment(this.path.segments.length / 2 - 2);
this.path.insert(0, newTop);
this.path.removeSegment(this.path.segments.length / 2);
this.path.insert(this.path.segments.length - 1, newBottom);

var newMiddleB = (this.path.segments[0].point + this.path.segments[
  this.path.segments.length - 2].point) / 2;
this.path.lastSegment.point = newMiddleB + this.gap[this.gap.length - 1];

var newMiddleF = (this.path.segments[this.path.segments.length / 2]
  .point + this.path.segments[this.path.segments.length / 2 - 2].point
) / 2;
this.path.segments[this.path.segments.length / 2 - 1].point =
  newMiddleF - this.gap[0];

```

Ok, now is is time to run a test.

https://www.youtube.com/watch?v=MJ2vEjRQbfA

Yeah, I bring my strokes wormy lives!
