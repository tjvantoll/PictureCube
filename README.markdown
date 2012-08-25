# PictureCube

Create a 3D interactive cube with an image on all 6 sides.  For a full explanation of the creation of this file and a full demo of all of the functionality see http://tjvantoll.com/2012/02/27/Making-a-3D-Picture-Cube-with-CSS3/.  [All browsers that support CSS 3D transforms](http://caniuse.com/#feat=transforms3d) are supported.

## Usage

Include the CSS and JS files.

    <link rel="stylesheet" href="/PictureCube.css" />
    <script src="/PictureCube.js"></script>

Call the constructor anytime after the appropriate DOM node that will contain the cube has been created.

* node `String`: The DOM node or the `id` of the DOM node to turn into the PictureCube.
* images `Array`: An array of `Object`s.  Each `Object` should have `src` and `id` attributes which will applied to the `<img />` tags created.
* options `Object`: An optional set of options to configure the cube.  Right now only an `onchange` event is available.

Example:

    <div id="cube"></div>

    <script>
        var cube = new PictureCube('cube',
            [
                { src: '1.jpg', title: 'Picture 1' },
                { src: '2.jpg', title: 'Picture 2' },
                { src: '3.jpg', title: 'Picture 3' },
                { src: '4.jpg', title: 'Picture 4' },
                { src: '5.jpg', title: 'Picture 5' },
                { src: '6.jpg', title: 'Picture 6' }
            ],
            {
                onchange: function(number, image, cube) {
                    console.log('Side # ' + number + ' is now showing');
                }
            }
        );
    </script>
    
    
Since PictureCube depends on CSS 3D transforms, you can use [Modernizr](http://modernizr.com) to detect support...

    if (Modernizr.csstransforms3d) {
        new PictureCube('', []);
    }
    
...but there's really no harm in calling PictureCube blindly.  Browsers that don't support 3D transforms will just get a box with the first image in the array passed in.
    
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
    
## Events

#### onchange

If you pass an `onchange` `function` to the constructor it will be invoked everytime the side of the cube displaying changes.  The `function` will be passed the following parameters.

* number `Number`: The side number displaying (1 - 6).
* image `DOMNode`: The `<img />` tag currently displaying.
* cube `PictureCube`: A reference to the `PictureCube` instance.

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