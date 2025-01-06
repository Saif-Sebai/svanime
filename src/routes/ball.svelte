<script lang="ts">
	import { browser } from '$app/environment';
	let x = 50; // Initial x position (percentage)
	let y = 50; // Initial y position (percentage)
	let angle = 0; // Initial angle

	// Update position in an ellipse
	const updatePosition = () => {
		const radiusX = 40; // Horizontal radius (percentage)
		const radiusY = 20; // Vertical radius (percentage)
		angle += 0.03; // Increment angle (adjust speed by changing this value)
		x = 50 + radiusX * Math.cos(angle); // Update x position
		y = 50 + radiusY * Math.sin(angle); // Update y position
	};

	if (browser) {
		function animate() {
			// Use requestAnimationFrame for smooth animations
			function frame() {
				updatePosition();

				// Call frame again to continue animation
				window.requestAnimationFrame(frame);
			}

			// Start the animation
			window.requestAnimationFrame(frame);
		}

		// Start animation when component is mounted
		animate();
	}
</script>

<img
	style="max-height:5%;top:{x}%;left:{y}%;position:absolute;"
	alt=""
	src="https://cdn.pixabay.com/animation/2024/02/27/22/48/22-48-46-412_256.gif"
/>
