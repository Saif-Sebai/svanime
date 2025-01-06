<script lang="ts">
	import { browser } from '$app/environment';
	let x = 30;
	let y = 10;
	let dx = 0.8;
	let dy = 0.7;
	if (browser) {
		function animate() {
			// Use requestAnimationFrame for smooth animations
			function frame() {
				x += dx;
				y += dy;

				if (x >= 90 || x <= 0) {
					dx *= -1;
				}
				if (y >= 90 || y <= 0) {
					dy *= -1;
				}

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
	style="max-height:10%;top:{x}%;left:{y}%;position:absolute;"
	alt=""
	src="https://www.gifservice.fr/img/gif-vignette-large/a6d3d0463855c0a5c5e6ecfc2366d5f0/273082-d-v-d-video-video-iconos-multimedia.gif"
/>
