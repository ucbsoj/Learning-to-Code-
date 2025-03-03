<script>
	import Hero from "$components/helpers/Hero.svelte";

	/* 
		The Hero component is a full-width image or video with a headline, dek, and byline (these are optional).
		- hed: The headline for the hero.
		- dek: The dek for the hero.
		- byline: The byline for the hero.
		- src: The source of the image or video file.
		- alt: The alt text, if it's an image.
	*/
</script>

<Hero
	hed="Super Commuters. The Long Journey Home"
	dek="Ever driven 90 minutes to work? These people do it every day."
	byline="By Andres Larios and Jessica Blough"
	src="assets/demo/test.jpg"
	alt="A lake and some clouds"
/>

<!-- Hero with video -->
<!-- <Hero
	hed="This is a placeholder headline"
	dek="Welcome to this demo"
	byline="By This Person and That Person"
	src="assets/demo/test.mp4"
	alt="Flourescent jellyfish moving around"
/> -->
