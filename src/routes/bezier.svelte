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
	points.push({ x: 900, y: 900 });
	points.push({ x: 1600, y: 700 });
	points.push({ x: 1020, y: 1080 - 900 });

	function bezier(t: number, p1: Point, p2: Point): Point {
		return {
			x: Number(((1 - t) * p1.x + t * p2.x).toFixed(5)),
			y: Number(((1 - t) * p1.y + t * p2.y).toFixed(5)) //ok maybe no need for toFixed...
		};
	}

	function drawLine(p1: Point, p2: Point): { length: number; angle: number } {
		let deltaX = p2.x - p1.x;
		let deltaY = p2.y - p1.y;
		return {
			length: Math.sqrt(deltaX ** 2 + deltaY ** 2),
			angle: Math.atan2(deltaY, deltaX) * (180 / Math.PI)
		};
	}

	function travel(t: number, points: Point[], pos: Point): [number, Point] {
		t += 0.01;
		q0 = bezier(t, points[0], points[1]);
		q1 = bezier(t, points[1], points[2]);
		pos = bezier(t, q0, q1);
		// console.log(t);
		if (t > 1) {
			console.log('GG');

			t = 0;
		}
		return [t, pos];
	}

	// Start the animation
	let t = 0;
	let q0 = bezier(t, points[0], points[1]);
	let q1 = bezier(t, points[1], points[2]);
	let b = bezier(t, q0, q1);
	let k = 0;
	let alpha = 0;

	function animate() {
		// Use requestAnimationFrame for smooth animations
		function frame() {
			// t = Math.cos(alpha);
			alpha += 0.01 * Math.PI;
			console.log(t);

			if (Math.sin(alpha) > 0) {
				let back = points.slice(2);
				back.push(points[0]);
				[t, b] = travel(t, back, b);
			} else {
				[t, b] = travel(t, points, b);
			}

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
<h1 style="max-height:10%;bottom:{points[0].y}px;left:{points[0].x}px;position:absolute;">O</h1>
<h1 style="max-height:10%;bottom:{points[1].y}px;left:{points[1].x}px;position:absolute;">O</h1>
<h1 style="max-height:10%;bottom:{points[2].y}px;left:{points[2].x}px;position:absolute;">O</h1>
<h1 style="max-height:10%;bottom:{points[3].y}px;left:{points[3].x}px;position:absolute;">O</h1>
<h1 style="max-height:10%;bottom:{q0.y}px;left:{q0.x}px;position:absolute;">O</h1>
<h1 style="max-height:10%;bottom:{q1.y}px;left:{q1.x}px;position:absolute;">O</h1>
