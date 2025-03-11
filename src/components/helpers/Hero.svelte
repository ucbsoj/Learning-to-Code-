<script>
	const { hed, dek, byline, src, alt } = $props();
</script>

<div class="hero">
	{#if src.endsWith(".mp4")}
		<video {src} autoplay loop muted playsinline></video>
	{:else}
		<img {src} {alt} />
	{/if}

	<div class="text">
		{#if hed}<h1>{@html hed}</h1>{/if}
		{#if dek}<h2>{@html dek}</h2>{/if}
		{#if byline}<p>{@html byline}</p>{/if}
	</div>
</div>

<style>
	.hero {
		width: 100vw;
		height: 100vh;
		position: relative;
	}

	img,
	video {
		height: 100%;
		width: 100%;
		object-fit: cover;
	}

	.text {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		color: white;
		background-color: #223240;
		background: rgba(0, 0, 0, 0.5);
		padding: 1rem 2rem;
		text-align: center;
	}
	h2 {
		font-size: 1rem; /* Adjust this value to change the size of the dek */
	}
</style>
