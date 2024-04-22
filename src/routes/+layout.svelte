<script lang="ts">
	import '../app.postcss';
	import { onMount } from 'svelte';

	onMount(() => {
		window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', (event) => {
			if (event.matches) {
				document.documentElement.classList.add('dark');
			} else {
				document.documentElement.classList.remove('dark');
			}
		});
	});
</script>

<slot />
