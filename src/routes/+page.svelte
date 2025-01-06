<script lang="ts">
	import Bezier from './bezier.svelte';
	import Dvd from './dvd.svelte';

	// This can be false if you're using a fallback (i.e. SPA mode)
	export const prerender = true;
</script>

<!-- <h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p> -->
<!-- <Dvd></Dvd> -->
<Bezier></Bezier>
