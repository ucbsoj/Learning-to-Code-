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
			<div
				class="step"
				class:first={i === 0}
				class:last={i === steps.steps.length - 1}
				class:left={i === 2 ||
					i === 4 ||
					i === 10 ||
					i === 11 ||
					i === 14 ||
					i === 17 ||
					i === 21}
				class:right={i === 5 ||
					i === 8 ||
					i === 13 ||
					i === 15 ||
					i === 16 ||
					i === 18 ||
					i === 19 ||
					i === 22}
				class:capitola={i === 8 || i === 9 || i === 10 || i === 11}
				class:center={i === 0 ||
					i === 1 ||
					i === 11 ||
					i === 9 ||
					i === 8 ||
					i === 11}
				class:tracy={i === 12 || i === 13 || i === 14}
				class:los={i === 15 || i === 16 || i === 17}
				class:medanos={i === 20 || i === 21 || i === 22}
				class:fish={i === 0 ||
					i === 1 ||
					i === 2 ||
					i === 3 ||
					i === 4 ||
					i === 5 ||
					i === 18 ||
					i === 19 ||
					i === 23 ||
					i === 24}
				data-step={i}
				class:hidden={i === 3 || i === 7}
				class:audio={i === 9 || i === 11 || i === 13 || i === 14 || i === 22}
			>
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
		height: 10vh;
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
	.first {
		margin-top: 0;
	}

	.last {
		margin-bottom: 200px;
	}

	.capitola {
		border: 3px solid #f86624;
	}

	.tracy {
		border: 3px solid #f9c80e;
	}
	.los {
		border: 3px solid #02c3bd;
	}
	.medanos {
		border: 3px solid red;
	}
	.fish {
		border: 3px solid #52647e;
	}

	.left {
		margin-left: 50px;
		max-width: 500px;
	}

	.right {
		margin-right: 50px;
		margin-left: 55.5vw;
	}
	.hidden {
		display: none;
	}
	.audio {
		padding-top: 0;
		padding-bottom: 0;
	}
	/* .center {false
	} */
	/* .red {
		border: 3px solid red;
	} */
</style>
