# Grunt

An automated task runner to do the things that web developers should be doing, but generally can't be hassled to while in a crunch


## Setup

npm cache clean
sudo npm install -g grunt-cli

Installs the grunt Command Line Utility (which is needed to run the tasks)


### Install a Grunt Plugin

npm install grunt-contrib-connect --save-dev

in the Gruntfile.js

grunt.loadNpmTasks('grunt-contrib-connect');



#### grunt-contrib-connect

This task creates a quick node server, convenient for testing static sites.

	connect: {
			server: {
				options: {
					port: 8181,
					base: 'dist'
				}
			}
		}
		
Server will close if grunt stops running, so just running grunt connect wont keep it up. It must be running with another task like grunt watch.

	grunt.registerTask('default', ['connect', 'watch']);
	
Or you can call it with a keep alive option, either setting it in the options or 

	grunt connect:server:keepalive
	

### grunt-browserify

Allows importing of javascript files in a nodelike structure. Bundles files. The browser itself does not understand 'require'. Browserfy is needed to compile these files and then spits out a 'bundle.js'.
	
math.js
	
	var math = {};

	math.add = function() {
		'use strict';
		var sum = 0, i = 0, args = arguments, l = args.length;
		while (i < l) {
			sum += args[i++];
		}
		return sum;
	};

	module.exports = math;
	
	
increment.js

	var add = require('./math').add;
	function inc(val) {
		'use strict';
		return add(val, 1);
	}
	module.exports = inc;	
	
main.js
	
	var inc = require('./inc');
	var a = 1;
	console.log( inc(a) );
	

if you were to just have 

	<script src="main.js"></script>
	
Then you would get errors because 'require' is not defined. It is not a function defined in JS and the browser doesn't know it. You need to compile the JS first.

	browserify main.js -o bundle.js
	then <script src="bundle.js"></script>
	
And it works!
	


### grunt-concurrent

Run multiple grunt tasks at the same time

### grunt-contrib-copy

Copy files, used to move files from a development location to Production/server location
  
### grunt-contrib-imagemin

Minifify images
  
### grunt-contrib-jshint

Lint Javascript files. 
    
### grunt-contrib-less

Compiles Less files to CSS files. 

### grunt-contrib-uglify

compress and minify javascript


### grunt-contrib-watch

Watches files for changes and can call other grunt tasks on change


### grunt-jsbeautifier

Cleans up your files via a .jsbeautifier file. Cleans up all indents, whitespace, brackets, etc. So all code looks consistence


### grunt-mocha-istanbul

Testing, Test Coverage, Reporting


### grunt-newer

Determine which files have been edited to speed up changes only on those.

### grunt-plato

Testing, Test Coverage, Reporting

### grunt-templater

Turns templates (ejs, jade)into standard HTML. 

### istanbul

Testing, Test Coverage, Reporting

### jade

### jshint-stylish

### mocha

### testem
    
    