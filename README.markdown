### PictureCube

Create a 3D picture cube with an image on all 6 sides.

<pre>
<script>
addEventListener('DOMContentLoaded', function() {
	var cube = new PictureCube('nodeToBecomeTheCube', [
		'1.jpg',
		'2.jpg',
		'3.jpg',
		'4.jpg',
		'5.jpg',
		'6.jpg'
	]);
	cube.cycle(2000);
});
</script>
<div id="nodeToBecomeTheCube"></div>
</pre>

TODO: Expand
TODO: Link to blog post