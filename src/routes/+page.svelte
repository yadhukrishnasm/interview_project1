<script>
	import { onMount } from 'svelte';
	import gsap from 'gsap';
	import ScrollTrigger from 'gsap/ScrollTrigger';
	import ScrollSmoother from 'gsap/ScrollSmoother';
	import Hero from '$lib/landing/hero.svelte';

	onMount(() => {
		gsap.registerPlugin(ScrollTrigger, ScrollSmoother);
		ScrollTrigger.default({
			toggleActions: 'restart pause resume pause',
			scroller: ' .smooth-content'
		});
		// Example animation using ScrollTrigger
		gsap.to('.page', {
			scrollTrigger: {
				duration: 2,
				repeat: 1
			}
		});
	});
</script>

<div id="smooth-wrapper">
	<div id="smooth-content">
		<div class="page bg-[#FAF9F6] text-2xl text-black" id="hero"><Hero /></div>
		<div class="page bg-black" id="about">about page</div>
		<div class="page" id="showcase"></div>
		<div class="page" id="review"></div>
		<div class="page" id="vision"></div>
		<div class="page" id="membership"></div>
		<div class="page" id="contact"></div>
		<div class="page" id="footer"></div>
	</div>
</div>

<style>
	.page {
		width: 100%;
		height: 100vh;
		position: relative;
		display: flex;
		align-items: center;
		overflow: hidden;
		scroll-snap-align: start;
	}
	#smooth-content {
		scroll-snap-type: y mandatory;
		overflow: auto;
		height: 100vh;
	}
</style>
