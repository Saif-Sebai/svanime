<script lang="ts">
	import Arrow from './arrow.svelte';
	import Ball from './ball.svelte';
	import Bezier from './bezier.svelte';
	import Dvd from './dvd.svelte';

	// This can be false if you're using a fallback (i.e. SPA mode)
	export const prerender = true;
</script>

<!-- <h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p> -->
<!-- <Dvd></Dvd> -->
<!-- <Bezier></Bezier> -->
<!-- <Ball></Ball> -->
<Arrow radiusX={30} radiusY={20} speed={0.05} rotate={1}>WHAAAAAAAAAAAT?</Arrow>
<Arrow radiusX={20} radiusY={20} speed={0.04}>
	<img alt="" src="https://media.tenor.com/L4ncxhqryfQAAAAj/cat.gif" />
</Arrow>

<Arrow radiusX={30} radiusY={60} speed={0.04} rotate={1}>
	<img alt="" src="https://media.tenor.com/gjTjxUCoP3sAAAAj/jumping-gatito.gif" />
</Arrow>
