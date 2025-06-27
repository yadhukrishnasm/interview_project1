<script>
	import { onMount } from 'svelte';

	const cardCount = 7;
	    const images = [
        "/images/12.jpg",
        "/images/13.jpg",
        "/images/14.jpg",
        "/images/15.jpg",
        "/images/16.jpg",
        "/images/19.jpg",
        "/images/21.jpg",
    ];

	onMount(async () => {
		const gsap = (await import('gsap')).default;
		const ScrollTrigger = (await import('gsap/ScrollTrigger')).default;
		gsap.registerPlugin(ScrollTrigger);

		const spread = 130; // distance between each card

		gsap.fromTo(
			".card",
			{
				x: 0,
				y: 0,
				rotate: 0,
				boxShadow: "0 0 0 rgba(0,0,0,0)",
			},
			{
				x: (i) => (i - (cardCount - 1) / 2) * spread,
				y: (i) => Math.abs(i - (cardCount - 1) / 2) * 10, 
				rotate: (i) => (i - (cardCount - 1) / 2) * 5,
				boxShadow: "20px 20px 34px rgba(0,0,0,0.15)",
                borderRadius: "10px",
				duration: 1.5,
				ease: "power3.out",
				stagger: 0.07,
				scrollTrigger: {
					trigger: "#showcaseContainer",
					start: "top 80%",
					scroller: "#smooth-content",
					toggleActions: "play none none none"
				}
			}
		);
	});
</script>

<div id="showcaseContainer" class="space-y-10 p-20 ">
	<div id="heading" class="text-center">
		<p class="text-center text-5xl">A place to display your <br /> Masterpiece</p>
	</div>
	<div id="Cards-container" class="relative h-[40vh]  flex items-center justify-center">
        {#each Array(cardCount) as _, i}
            <div class="card absolute h-48 w-48 border bg-white">
                <img src={images[i]} alt="Artwork {i + 1}" class="object-cover w-full h-full rounded-[10px]" />
            </div>
        {/each}
	</div>
	<div id="subheading" class="space-y-2 text-center">
		<p class="text-center">
			Artists put it out there. The lovers will love, the haters will hate <br /> and someone's uncle
			will compare it to a mango.
		</p>
		<button class="mr-7 rounded-full border px-3 py-2">Login/Register</button>
		<button class="">Read more</button>
	</div>
</div>

<style>
	#Cards-container {
		width: 100%;
	}
	.card {
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
		transition: box-shadow 0.3s;
	}
</style>
