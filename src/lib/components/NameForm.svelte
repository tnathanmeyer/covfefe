<script lang="ts">
	import { TRANSITION_TIME } from '$lib/constants';

	export let name: string;

	let opacity3 = 100;
	let formHeight = '160px';
	let showButton = true;

	function hideButton() {
		opacity3 = 0;
		formHeight = '102px';

		setTimeout(() => {
			showButton = false;
		}, TRANSITION_TIME);
	}
</script>

<form
	on:submit={hideButton}
	class="h-[{formHeight}] transition-all ease-in duration-{TRANSITION_TIME} w-full card p-4 text-token space-y-4"
>
	<label class="label">
		<span>What is your name?</span>
		<input class="input" type="text" bind:value={name} required />
	</label>
	{#if showButton}
		<div class="text-right opacity-{opacity3}">
			<button type="submit" class="btn variant-outline">Submit</button>
		</div>
	{/if}
</form>
