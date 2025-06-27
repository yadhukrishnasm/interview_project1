<script>
	import { onMount } from 'svelte';
	import gsap from 'gsap';
	import ScrollTrigger from 'gsap/ScrollTrigger';
	import ScrollSmoother from 'gsap/ScrollSmoother';
	import Hero from '$lib/landing/hero.svelte';
	import About from '$lib/landing/about.svelte';
	import Showcase from '$lib/landing/showcase.svelte';
	import Review from '$lib/landing/review.svelte';
	import Footer from '$lib/landing/footer.svelte';

	onMount(() => {
		gsap.registerPlugin(ScrollTrigger, ScrollSmoother);
		ScrollTrigger.defaults({
			toggleActions: 'restart pause resume pause',
			scroller: '#smooth-content' // <-- fix selector
		});
	});
</script>

<div id="smooth-wrapper">
	<div id="smooth-content">
		<div class="page text-2xl text-black" id="hero"><Hero /></div>
		<div class="page" id="about"><About /></div>
		<div class="page" id="showcase"><Showcase /></div>
		<div class="page" id="review"><Review /></div>
		<div class="page p-4" id="footer"><Footer /></div>
	</div>
</div>

<style>
	.page {
		width: 100%;
		height: 100vh;
		position: relative;
		overflow: hidden;
		background-color: #f9eae1;
		scroll-snap-align: start;
	}
	#smooth-content {
		scroll-snap-type: y mandatory;
		overflow: auto;
		height: 100vh;
	}
</style>
