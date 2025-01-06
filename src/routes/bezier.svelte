<script lang="ts">
	import { browser } from '$app/environment';
	import { sineIn } from 'svelte/easing';
	type Point = {
		x: number;
		y: number;
	};
	let points: Point[] = [];
	// 1920 x 1080
	points.push({ x: 200, y: 200 });
	points.push({ x: 900, y: 1600 });
	points.push({ x: 1900, y: 700 });
	points.push({ x: 1020, y: 1080 - 900 });
	points.push(points[0]);
	points.push(points[2]);
	// points.push(points[1]);

	/**
	 * Linear interpolation between two points.
	 */
	function lerp(t: number, p0: Point, p1: Point): Point {
		return {
			x: (1 - t) * p0.x + t * p1.x,
			y: (1 - t) * p0.y + t * p1.y
		};
	}

	/**
	 * Generalized Bézier function for n control points.
	 */
	function bezier(t: number, controlPoints: Point[]): Point {
		if (controlPoints.length === 1) {
			return controlPoints[0];
		}

		const newPoints: Point[] = [];
		for (let i = 0; i < controlPoints.length - 1; i++) {
			newPoints.push(lerp(t, controlPoints[i], controlPoints[i + 1]));
		}

		return bezier(t, newPoints); // Recursive call
	}

	function drawLine(p1: Point, p2: Point): { length: number; angle: number } {
		let deltaX = p2.x - p1.x;
		let deltaY = p2.y - p1.y;
		return {
			length: Math.sqrt(deltaX ** 2 + deltaY ** 2),
			angle: Math.atan2(deltaY, deltaX) * (180 / Math.PI)
		};
	}

	// function travel(t: number, points: Point[], pos: Point): [number, Point] {
	// 	t += 0.01;
	// 	q0 = bezier(t, points[0], points[1]);
	// 	q1 = bezier(t, points[1], points[2]);
	// 	pos = bezier(t, q0, q1);
	// 	// console.log(t);
	// 	if (t > 1) {
	// 		console.log('GG');

	// 		t = 0;
	// 	}
	// 	return [t, pos];
	// }

	// Start the animation
	let t = 0;
	// let q0 = bezier(t, points[0], points[1]);
	// let q1 = bezier(t, points[1], points[2]);
	// let b = bezier(t, q0, q1);
	let k = 0;
	let alpha = 0;
	let b: Point = points[0];

	function animate() {
		// Use requestAnimationFrame for smooth animations
		function frame() {
			// t = Math.cos(alpha);
			t += 0.01;
			if (t > 1) {
				t = 0;
			}
			b = bezier(t, points);

			window.requestAnimationFrame(frame);
			// [t, b] = travel(t, points, b);

			// points.push(points[0]);
			// travel(t, points.slice(2));
			// Call frame again to continue animation
		}

		// Start the animation
		let t = 0;
		window.requestAnimationFrame(frame);
	}

	if (browser) {
		// Start animation when component is mounted
		animate();
	}
</script>

<img
	style="max-height:10%;bottom:{b.y - 20}px;left:{b.x - 150}px;position:absolute;"
	alt=""
	src="https://www.gifservice.fr/img/gif-vignette-large/a6d3d0463855c0a5c5e6ecfc2366d5f0/273082-d-v-d-video-video-iconos-multimedia.gif"
/>
<h1 style="max-height:10%;bottom:{points[0].y}px;left:{points[0].x}px;position:absolute;">.</h1>
<h1 style="max-height:10%;bottom:{points[1].y}px;left:{points[1].x}px;position:absolute;">.</h1>
<h1 style="max-height:10%;bottom:{points[2].y}px;left:{points[2].x}px;position:absolute;">.</h1>
<h1 style="max-height:10%;bottom:{points[3].y}px;left:{points[3].x}px;position:absolute;">.</h1>
<!-- <h1 style="max-height:10%;bottom:{q0.y}px;left:{q0.x}px;position:absolute;">O</h1> -->
<!-- <h1 style="max-height:10%;bottom:{q1.y}px;left:{q1.x}px;position:absolute;">O</h1> -->
