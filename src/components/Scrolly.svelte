<script>
	import Mapbox from "$components/Mapbox.svelte";
	import Audio from "$components/Audio.svelte";
	import Scrolly from "$components/helpers/Scrolly.svelte";
	import steps from "$data/steps.json";

	/*
		Scrolly is a component that allows you to create a scrollytelling effect.
		- value: Takes on the value of the current scroll step that's most in view.

		When using Scrolly, create a container with the class "sticky" and the CSS in the example below.
		That will create a sticky container that will stay in place while the steps scroll over it.
	*/

	let value = $state();
	// $inspect(value);

	let components = {
		Audio
	};
</script>

<section id="scrolly">
	<div class="sticky">
		<Mapbox {value} />
	</div>
	<div class="spacer"></div>

	<Scrolly bind:value>
		{#each steps.steps as step, i}
			<div class="step">
				{#each step.content as { type, value }}
					{@const C = components[type]}
					{@const isString = typeof value === "string"}
					{#if C}
						<C {...value} />
					{:else if type === "text"}
						<p>{@html value}</p>
					{:else if isString}
						<svelte:element this={type}>
							{@html value}
						</svelte:element>
					{:else}
						<svelte:element this={type} {...value}></svelte:element>
					{/if}
				{/each}
			</div>
		{/each}
	</Scrolly>

	<div class="spacer"></div>
</section>

<style>
	.sticky {
		position: sticky;
		top: 0;
		height: 100vh;
		z-index: -1;
	}

	.spacer {
		height: 50vh;
	}

	.step {
		margin: 100vh 20vw;
		background: var(--color-gray-100);
		text-align: center;
		padding: 1rem 2rem;
		/* background-image: url("/assets/commute-images/gps.svg");
		background-size: cover;
		background-position: center;
		background-repeat: no-repeat; */
	}

	.step p {
		padding: 1rem;
	}

	span {
		background: var(--color-mark);
		padding: 0 8px;
	}
</style>
