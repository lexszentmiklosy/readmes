#Canvas

HTML

```
	<canvas id="MyCanvas" width="500" height="500">
		This text renders on browsers that do not support Canvas elements
	</canvas>
	
```

JS 

```
	var canvas = document.getElementById('MyCanvas');
	
	//Canvas has a context, 2d or  "experimental-webgl" which changes how it renders
	
	var c = canvas.getContext('2d');
	
	
	//Fill the canvas
	
	c.fillStyle = "black";
	
	startX, StartY, Width, Height
	c.fillRect(0, 0, canvas.width, canvas.height);
	
	c.strokeStyle = "white";
	c.lineWidth = 10;
	c.strokeRect = (20, 20, 50, 50);
	
	
	c.beginBath();
	// Lift pen and place it, no drawing
	c.moveTo(100,100);
	c.lineTo(150, 200);
	c.lineTo(250, 100);
	c.closePath();
	
	// Order changes what is on top
	c.stroke(); 
	c.fill();
	
	c.fill();
	c.stroke();
	
	
	c.font = "20px Helvetica";
	c.fillStyle = 'white';
	//String, xPos, yPos;
	c.fillText("Hello", 200, 200);
	
	
	c.beginPath();
	
	// X, Y, radius, Starting point (0 radians is the top), Math.PI * 2 (how many radians clockwise), false);
	c.arc(200, 300, 50, 0, Math.PI * 2, false);
	c.fill();
	
	var xPos = 0;
			
	setTimeout(function() {
		xPos += 1;
		
		c.fillStyle = "black";
		c.fillRect(0, 0, canvas.width, canvas.height);
		
		c.beginPath();
		c.arc(xPos, 300, 50, 0, Math.PI * 2, false);
		c.fill();		
		
	}, 30);
	
	
	
	
	
	
	
```


Don't just run in an infinante loop 


```

	while(true) {
		//do stuff
	}

```

Don't quite do this either...

```

	function animate() {
		context.clearRect(0,0, canvas.width, canvas.height);
		update();
		draw();
	}
	
	setInterval(animate, 1000/ 60); // 60fps?
	
	setInterval is allowed to be padded by the Browser, it will not be as milisecond specific as intended
	

```


Let the browser decide when to draw the next frame

```

	function animate() {
		context.clearRect(0,0, canvas.width, canvas.height);
		update();
		draw();
		
		if( window.webkitRequestAnimationFrame !== undefined) 		{
			window.webkitRequestAnimationFrame(animate);
		}
	}
	
	
	if( window.webkitRequestAnimationFrame !== undefined) {
			window.webkitRequestAnimationFrame(animate);
		}
		
		
```

There is a polyfill for this for to support multiple browsers not just Webkit



# Calulate FPS



``` 

	function calculateFPS() {
	var now = +new DAte(),
		fps = 1000 / (now - lastTime);
		
	lastTime = now;
	
	return fps;

```


You need time based motion! Not frame based! Things will be more jumpy but you will get similar results across all browsers and computers

If you use frame based motion, for example move left 3 px every frame and your frame rate slows down things will move slowly

if you use time based and say move 3 px left every 10ms it will be consistent (but possibly jumpy)	

Will screw up collision detection otherwise 

Should pause things on window.blur() (not in focus or current tab). and get current time, subjtract time of unpause to not

Calculating Pixels/frame

```

	var numDiscs = 3;
	
	function updateTimeBased() {
		var i = numDiscs, disc = null;
		
		while (i--) {
		disc = discs[i];
		//current FPS was set before this method was called
		
		deltaX = disc.velocityX / currentFPS;
		deltaY = disc.velocityY / currentFPS;
		
		disc.x += deltaX
		disc.y += deltaY
	}
	
	
```

60fps = 16.7ms per frame


//Some how has the best performance
1) Erase everything and redraw everything for every animation frame


//These work if the background is more complicated and movement is complex
2) Move things and restore the backround undernearth (Clipping)

3) Blit from an offscreen canvas, Use a secondary canvas (Copy background from offscreen campus where the animation takes place)


DevTools

Profiles and Timelines
How much time is spent in each JS function


Animation Best Practices:

* Use profiling and timelines to monitor and improve performance
* Clip when you are animating a small number of objects, otherwise redraw everything
* Don't double buffer (make a second canvas and copy it back). Canvas already buffers
* Avoid CSS Shadows and Rounded corners when possible
* Avoid Canvas Shadows when possible
* Let the browser decide when to animate (window.RequestAnimationFrame)
* Avoid allocating memory during animations
* use time based animation



[Save Restore](http://html5.litten.com/understanding-save-and-restore-for-the-canvas-context/)
context.save()
context.restore()


Collision Detection - Seperating Axis Theorem (SAT)


Projections, Shine the light, if their shadows overlap then they have colided. SAT Tests all axes


Bounded Boxes for simpler collision detection

(Add behavior to sprites)


Unity, Unity3d, ImpactJS



# HTML5 Game Development for Beginners Videos


Key Event listeners

```

var keys =  [];

window.addEventListener('keydown', function(e){
    keys[e.keyCode] = true;
}, false);


window.addEventListener('keyup', function(e){
    delete keys[e.keyCode];
});

```


/*
up 38 W 87
down 40 S 83 
left 37 A 65 
right 39 D 68
space 32
*/


```
var canvas = document.getElementById('MyCanvas');
var c = canvas.getContext('2d');
var keys = [];
var background = 'cornflowerblue';
var speed = 3;
var score = 0;



var player = {
    x: 10,
    y: 10,
    width: 20,
    height: 20
};

var cube = {
    x: Math.random()* ( canvas.width - 20),
    y: Math.random()* ( canvas.height - 20),
    width: 20,
    height: 20
};




window.addEventListener('keydown', function(e){
    'use strict';

    keys[e.keyCode] = true;
}, false);


window.addEventListener('keyup', function(e){
    'use strict';
    delete keys[e.keyCode];
});

function collision(first, second) {
    'use strict';
    return !(
        first.x  > second.x + second.width ||
        first.x + first.width < second.x ||
        first.y > second.y + second.height ||
        first.y + first.height < second.y
        );
}

function process() {
    'use strict';
    score += 1;
    cube.x = Math.random()* ( canvas.width - 20);
    cube.y =  Math.random()* ( canvas.height - 20);
}


function movePlayer() {
    'use strict';
    // Move Player
    if (keys[38]) {player.y -= speed; }
    if (keys[40]) {player.y += speed; }
    if (keys[37]) {player.x -= speed; }
    if (keys[39]) {player.x += speed; }

    // Keep Player in Boundries
    if (player.x <= 0 ) { player.x = 0; }
    if (player.y <= 0 ) { player.y = 0; }

    if ( (player.x +player.width) >= canvas.width) {
        player.x = canvas.width - player.width;
    }

    if ( (player.y + player.height) >= canvas.height) {
        player.y = canvas.height - player.height;
    }

}

function moveCube() {
    'use strict';

    if (keys[87]) {cube.y -= speed; }
    if (keys[83]) {cube.y += speed; }
    if (keys[65]) {cube.x -= speed; }
    if (keys[68]) {cube.x += speed; }

    // Keep cube in Boundries
    if (cube.x <= 0 ) { cube.x = 0; }
    if (cube.y <= 0 ) { cube.y = 0; }

    if ( (cube.x +cube.width) >= canvas.width) {
        cube.x = canvas.width - cube.width;
    }

    if ( (cube.y + cube.height) >= canvas.height) {
        cube.y = canvas.height - cube.height;
    }

}

function update() {
    'use strict';

    movePlayer();
    moveCube();

    if ( collision(player, cube) ) {
        process();
    }
}





function render() {
    'use strict';

    // c.clearRect(0,0, canvas.width, canvas.height);
    c.fillStyle = background;
    c.fillRect(0,0, canvas.width, canvas.height);

    c.fillStyle = 'black';
    c.fillRect(player.x, player.y, player.width, player.height);

    c.fillStyle = 'green';
    c.fillRect(cube.x, cube.y, cube.width, cube.height);

    c.font = '20px Helvetica';
    c.fillStyle = 'white';
    c.fillText('Score: ' + score, 400, 30);

}

function game() {
    'use strict';
    update();
    render();
}

setInterval(function() {
    'use strict';
    game();

}, 1000/ 60); // 60~ fps
```


[http://jlongster.com/Making-Sprite-based-Games-with-Canvas](http://jlongster.com/Making-Sprite-based-Games-with-Canvas)


```
// The main game loop
var lastTime;
function main() {
    var now = Date.now();
    var dt = (now - lastTime) / 1000.0;

    update(dt);
    render();

    lastTime = now;
    requestAnimFrame(main);
};

```


Never ever use setInterval(main, 1000 / 60), as it's less accurate and also wastes a lot of cycles by rendering when unnecessary.

The update function takes the time that has changed since the last update. Never update your scene with constant values per frame (like x += 5;). Your game will run wildly different on various computers and platforms, so you need to update your scene independently of framerate.

This is achieved by calculating the time since last update (in seconds), and expressing all movements in pixels/second units. Movement then becomes x += 50 * dt, or "50 pixels per second".



var ctx = document.getElementById('myCanvas').getContext('2d');

//You don't need to set canvas to a varaible.
ctx.canvas.id, ctx.canvas.width 

ctx.fillStyle = color, hex, rgba(), gradient, pattern
ctx.fillStyle = 'white', '#ff4', 'rgba(255,255 0, .5)',


//gradient position is relative to canvas. needs to be set the same as the element you are filling for expected results
var gradient = ctx.createLinearGradient(x0, y0, x1, y1);

gradient.addColorStop( 0, "magenta");
gradient.addColorStop( 1, "black");

radialGradient

Paterns



Line Properties

ctx.lineCap = 'round'; //butt, round, square
ctx.lineJoin = 'miter'; //bevel, round, miter
ctx.miterLimit = 5;

ctx.setLineDash([20, 10, 30]);
ctx.lineDashOffset = 30; //moves tart of dashed line, can be used to 'march ants'
ctx.getLineDash();

ctx.lineWidth = 10;
ctx.strokeStyle = 'red'


ctx.isPointInPath(x, y);



//copy a 50x50 rectangle 
var src = ctx.getImageData(20, 20, 50, 50);
ctx.putImageData(250, 50)


var copy = ctx.credateImageData(src.width, src.height);
or
var copy = ctx.credateImageData(src);

//Copy image data
for var(i = 0; i< copy.data.length; i++) {
	copy.data[i] = src.data[i];
}

//Better way to copy array but isn't supported by IE...9?
copy.data.set(src.data);

ctx.putImageData(copy, 250, 20);


ctx.globalAlpha = 0 - 1;
ctx.CompositeOperation = (different masking and sort of z-index effects)


	