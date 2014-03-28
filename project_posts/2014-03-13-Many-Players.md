Now I’m considering multi-players. I have to think about many possible situations, like one laptop with many touch devices, many laptops with many touch devices, etc.

I come down to the strategy that dividing all the clients into two categories: touch-based, and desktop computer.
Touch-based devices are responsible for drawing static images, detecting motion events, and emitting data when being shook.
Desktop computers are here for receiving data from touch-based devices, and animating them.
Last but not least, desktop computer can also draw stroke and broadcasts its data to all the other laptops!

This sorting procedure is being done on the server side, I will send out a data of what type of device the client is when initiated.
The server has to mark down its type, so as to treat them differently later.
The diagram is like this:
![Socket](../project_images/socket.jpg?raw=true "Socket")

The code on the server side:
```
var laptopId = [];
sio.sockets.on('connection', function (socket) {

  socket.on('deviceData', function (data) {
    if (!data.device) {
      laptopId.push(socket.id);
    }
  });

  socket.on('mobileWorm', function (data) {
    laptopId.forEach(function (id) {
      sio.sockets.socket(id).emit('hisMobileWorm', data);
    });
  });

  socket.on('laptopWorm', function (data) {
    laptopId.forEach(function (id) {
      if (id !== socket.id) {
        sio.sockets.socket(id).emit('hisLaptopWorm', data);
      }
    });
  });

});

```
A quick test:
https://www.youtube.com/watch?v=Ew-45WwL0Zc
