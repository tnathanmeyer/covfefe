<script lang="ts">
	const TRANSITION_TIME = 500;
	let opacity1 = 0;
	let opacity2 = 100;
	let name = '';
	let stage = 0;

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

<div class="w-screen container h-full mx-auto flex justify-center items-center">
	<div class="w-3/4 md:w-1/2 lg:w-1/3">
		<div class="space-y-5 transition-all ease-in duration-1000 opacity-{opacity1}">
			<h1 class="h1">Hello</h1>
			<div class="space-y-5 transition-all ease-in duration-{TRANSITION_TIME} opacity-{opacity2}">
				{#if stage === 0}
					<form on:submit={nextStage} class="w-full card p-4 text-token space-y-4">
						<label class="label">
							<span>What is your name?</span>
							<input class="input" type="text" bind:value={name} required />
						</label>
						<div class="text-right">
							<button type="submit" class="btn variant-outline">Submit</button>
						</div>
					</form>
				{:else if stage === 1}
					<p>Welcome, {name}</p>
					<p>Today, we're going to choose your coffee gear.</p>
				{:else}
					<h3 class="h3">Brewer Types</h3>
					<div class="w-full grid grid-cols-1 md:grid-cols-2 gap-4">
						<div class="card bg-initial overflow-hidden card-hover">
							<img
								class="w-full aspect-[1/1] object-cover"
								src="https://aeropress.com/cdn/shop/files/APpresserAmazonheroimages_20231119-23_1300x.jpg?v=1700437038"
								alt="Aeropress"
							/>
							<!-- <section class="p-4">
							Aeropress
						</section> -->
						</div>
						<div class="card bg-initial p-4 flex justify-center items-center">Hario V60</div>
					</div>
				{/if}
			</div>
		</div>
	</div>
</div>
