# PictureCube

Create a 3D interactive cube with an image on all 6 sides.  For a full explanation of the creation of this file and a full demo of all of the functionality see http://tjvantoll.com/2012/02/27/Making-a-3D-Picture-Cube-with-CSS3/.  [All browsers that support CSS 3D transforms](http://caniuse.com/#feat=transforms3d) are supported.  Browsers that do not support the transforms will simply see a box with the first image passed in.

## Usage

Include the CSS and JS files.

	<link rel="stylesheet" href="/PictureCube.css" />
	<script src="/PictureCube.js"></script>

Call the constructor anytime after the 'DOMContentLoaded' event has fired.

	/**
	 * @param node {DOMNode|string} The node to turn into the cube or the id attribute of the node
	 * @param images {Array} An Array of 6 Strings containing the URLs of the images to place in the cube
	 */
	addEventListener('DOMContentLoaded', function() {
		var cube = new PictureCube('nodeToBecomeTheCube', [
			'1.jpg',
			'2.jpg',
			'3.jpg',
			'4.jpg',
			'5.jpg',
			'6.jpg'
		]);
	});
	
Since PictureCube depends on CSS 3D transforms, you can use [Modernizr](http://modernizr.com) to detect support...

	if (Modernizr.csstransforms3d) {
		new PictureCube('', []);
	}
	
but there's really no harm in calling PictureCube blindly.  Browsers that don't support 3D transforms will just get a box with the first image in the array passed in.
	
## Methods

goto - Go to a particular side of the cube using a 3D transformation.

	/**
	 * @param side {number} The number of the side to change the cube to (1 - 6).
	 */
	cube.goto(2);
	
cycle - Create an interval to cycle through the sides of the cube.

	/**
	 * @param interval {number} The number of milliseconds between each image transition
	 */
	 cube.cycle(2000);
	 
clearCycle - Clear the interval created by cycle.

	cube.clearCycle();

## Extendable

The following technique can be used to extend PictureCube.  This example creates an AwesomeCube that inherits the base methods from PictureCube's prototype.

	AwesomeCube = function(node, images) {
	    PictureCube.apply(this, [node, images]);
	};
	AwesomeCube.prototype = new PictureCube();
	AwesomeCube.prototype.newMethod = function() {
	    //this.cube, this.images, this.goto, this.cycle
	    //and this.clearCycle are available to the new
	    //function.
	};

## Limitations

Currently the cube will be 100px x 100px and will resize the images provided to be the same size.  Look for the size to be configurable in a future update.