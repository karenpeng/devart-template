The next step is to augment this magic moment when the drawing transforms from static to dynamic.

My idea is that it keeps still in a touch-based device, and comes vivid in a large desktop computer screen.
What serves as the trigger?
Shake you smart phone!

I begin to search for methods that detect motion of mobile devices, and I find this <a href="http://www.html5rocks.com/en/tutorials/device/orientation/">article</a> about DeviceMotionEvent.
From which I know that, what really works is an event handler:
```
function deviceMotionHandler(eventData) {
  var info, xyz = "[X, Y, Z]";

  // Grab the acceleration from the results
  var acceleration = eventData.acceleration;
  info = xyz.replace("X", acceleration.x);
  info = info.replace("Y", acceleration.y);
  info = info.replace("Z", acceleration.z);
}

```

Therefore I set a threshold for its xyz data, when it exceeds them, it shows that the phone is shaking.
```
function ifShake(x, y, z) {
  if (Math.abs(preX - x) > 10) {
    exports.shake = true;
    preX = x;
  } else if (Math.abs(preY - y) > 10) {
    exports.shake = true;
    preY = y;
  } else if (Math.abs(preZ - z) > 10) {
    exports.shake = true;
    preZ = z;
  } else {
    exports.shake = false;
  }
}

```

Ok, now I write a function emitting data from the mobile phone to the laptop when shaking is detected.
At the same time, the original strokes on your phone are deleted so as to create a feeling that the drawing goes from one place to another.
```
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
```

When the laptop receives the data, it starts to animate the strokes.
And I test and modify for several times until the threshold of the motion detection works well.

https://www.youtube.com/watch?v=Qh5C9Y6ZMPo
