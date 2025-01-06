<script lang="ts">
	import { browser } from '$app/environment';

	export let radiusX: number = 30; // Horizontal radius (percentage)
	export let radiusY: number = 20; // Vertical radius (percentage)
	export let speed: number = 0.05; // Speed of the animation
	export let rotate: number = 0;
	let x = 50; // Initial x position (percentage)
	let y = 50; // Initial y position (percentage)
	let angle = 0; // Initial angle
	let rotation = 0; // Initial rotation angle for the arrow

	// Update position and rotation in an ellipse
	const updatePosition = () => {
		// const radiusX = 30; // Horizontal radius (percentage)
		// const radiusY = 20; // Vertical radius (percentage)
		// const speed = 0.05; // Speed of the animation

		angle += speed; // Increment angle

		// Update position
		x = 50 + radiusX * Math.cos(angle);
		y = 50 + radiusY * Math.sin(angle);

		// Calculate the tangent angle (derivative)
		const dx = -radiusX * Math.sin(angle); // dx/dt
		const dy = radiusY * Math.cos(angle); // dy/dt
		rotation = rotate * Math.atan2(dy, dx) * (180 / Math.PI); // Convert to degrees
	};

	// Start animation loop
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

<div
	style="top:{y}%; left:{x}%; transform: translate(-50%, -50%) rotate({rotation}deg); skewX({50}deg);"
	class="rotating"
>
	<slot></slot>
</div>

<style>
	.rotating {
		position: absolute;
		transform: translate(-50%, -50%);
		transition: transform 0.016s linear; /* Smooth rotation */
	}
</style>
