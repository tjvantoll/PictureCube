# PictureCube

Create a 3D interactive cube with an image on all 6 sides.  For a full explanation of the creation of this file and a full demo of all of the functionality see tjvantoll.com.

## Usage

Call the constructor after the 'DOMContentLoaded' event has fired.

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