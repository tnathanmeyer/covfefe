<script lang="ts">
	import { NameForm } from '$lib/components';
	import { TRANSITION_TIME } from '$lib/constants';

	let opacity1 = 0;
	let opacity2 = 100;
	let name = '';
	let stage = 0;
	let aeropress = false;
	let v60 = false;

	setTimeout(() => (opacity1 = 100), 250);

	function nextStage() {
		opacity2 = 0;

		setTimeout(() => {
			++stage;
			opacity2 = 100;
		}, TRANSITION_TIME);
	}

	$: if (stage === 1) setTimeout(nextStage, 3000);
</script>

<!-- with button, 160px
	without button, 102px -->

<div class="w-screen container h-full mx-auto flex justify-center items-center">
	<div class="w-3/4 md:w-1/2 lg:w-1/3">
		<div class="space-y-5 transition-all ease-in duration-1000 opacity-{opacity1}">
			<h1 class="h1">Hello</h1>
			<div class="space-y-5 transition-all ease-in duration-{TRANSITION_TIME} opacity-{opacity2}">
				{#if stage === 0}
					<NameForm {name} />
				{:else if stage === 1}
					<p>Welcome, {name}</p>
					<p>Today, we're going to choose your coffee gear.</p>
				{:else if stage === 2}
					<h3 class="h3">Select your brewers</h3>
					<form on:submit={nextStage} class="w-full card p-4 space-y-4">
						<p>First, select which brewers you would like to use</p>
						<div class="space-y-2">
							<label class="flex items-center space-x-2">
								<input class="checkbox" type="checkbox" bind:checked={aeropress} />
								<p>Aeropress</p>
							</label>
							<label class="flex items-center space-x-2">
								<input class="checkbox" type="checkbox" bind:checked={v60} />
								<p>Hario V60</p>
							</label>
							<div class="text-right">
								<button type="submit" class="btn variant-outline">Submit</button>
							</div>
						</div>
					</form>
				{:else if stage === 3}
					{#if aeropress}
						<p>You chose Aeropress, nice</p>
					{/if}
					{#if v60}
						<p>You chose v60, are you sure?</p>
					{/if}
				{/if}
			</div>
		</div>
	</div>
</div>
