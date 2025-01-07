<script lang="ts">
	import Arrow from './arrow.svelte';
	import Ball from './ball.svelte';
	import Bezier from './bezier.svelte';
	import Dvd from './dvd.svelte';
	import catGif from '$lib/cats/giphy.webp';

	// This can be false if you're using a fallback (i.e. SPA mode)
	export const prerender = true;
</script>

<!-- <h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p> -->
<!-- <Dvd></Dvd> -->
<!-- <Bezier></Bezier> -->
<!-- <Ball></Ball> -->
<Arrow radiusX={30} radiusY={20} speed={0.05} rotateInner={1}>WHAAAAAAAAAAAT?</Arrow>
<Arrow radiusX={20} radiusY={20} speed={0.04}>
	<img alt="" src="https://media.tenor.com/L4ncxhqryfQAAAAj/cat.gif" />
</Arrow>

<Arrow radiusX={20} radiusY={60} speed={0.04} rotationDeg={45}>
	<img alt="" src="https://media.tenor.com/gjTjxUCoP3sAAAAj/jumping-gatito.gif" />
</Arrow>

<Arrow radiusX={0} radiusY={0} speed={0.04} rotationDeg={45}>
	<img
		style="max-width: 500px;"
		alt=""
		src="https://64.media.tumblr.com/e642b66f8548fa1485621bd82d3eacc9/df8c8427627025f7-72/s640x960/af7dc108c6fd722e684f767aa7ad6b9f72f9d9c9.gifv"
	/>
</Arrow>

<img
	src="https://media.tenor.com/OdAnooj4VlIAAAAj/placek-placek-transparent.gif"
	alt=""
	style="bottom:0%; left:0%;position:absolute;"
	class=""
/>

<img
	src="https://i.giphy.com/eLv7gJpxqiQtbNNQUe.webp"
	alt=""
	style="top:0%; right:0%;position:absolute; max-width:200px"
	class=""
/>

<img src={catGif} alt="" style="bottom:-2%; right:0%;position:absolute; max-width:200px" class="" />

<style>
	:global(body) {
		overflow: hidden; /* Hide scrollbars */
	}
</style>
