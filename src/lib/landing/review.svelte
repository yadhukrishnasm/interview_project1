<script>
	import { onMount } from 'svelte';

	const reviews = [
		{
			review:
				'mollitia dicta obcaecati reprehenderit commodi fugafacere veritatis reiciendis culpa consectetur sequi animi',
			rating: 5,
			src: '/images/p1.jpg'
		},
		{
			review: 'mollitia dicta obcaecati repreitatis reiciendis culpa consectetur sequi animi',
			rating: 4,
			src: '/images/p2.jpg'
		},
		{
			review: 'mollitia dicta re veritatis reiciendis culpa consectetur sequi animi',
			rating: 5,
			src: '/images/p3.jpg'
		}
	];

	let gsap;
	onMount(async () => {
		gsap = (await import('gsap')).default;
	});

	function handleMouseEnter(event, i) {
		const group = event.currentTarget.parentElement;
		const quote = group.querySelector('.quote-icon');
		gsap.to(event.currentTarget, {
			x: 40,
			scale: 1.04,
			boxShadow: '0 8px 24px rgba(0,0,0,0.18)',
			duration: 0.5,
			ease: 'power2.out'
		});
		gsap.to(quote, {
			rotate: 20,
			scale: 1.2,
			duration: 0.5,
			ease: 'power2.out'
		});
	}

	function handleMouseLeave(event, i) {
		const group = event.currentTarget.parentElement;
		const quote = group.querySelector('.quote-icon');
		gsap.to(event.currentTarget, {
			x: 0,
			scale: 1,
			boxShadow: '0 2px 8px rgba(0,0,0,0.08)',
			duration: 0.5,
			ease: 'power2.inOut'
		});
		gsap.to(quote, {
			rotate: 0,
			scale: 1,
			duration: 0.5,
			ease: 'power2.inOut'
		});
	}
</script>

<div id="review-containter" class="h-full grid-cols-2 items-center justify-center md:grid">
	<div class="mt-10 flex flex-col space-y-2 px-5 py-10 md:mt-0 md:p-20">
		<p class="text-5xl font-instrument">What Our  Customers Say</p>
		<p>
			Lorem, ipsum dolor sit a obcaecati reprehenderit commodi fuga facere veritatis reiciendis
			culpa consectetur sequi animi.
		</p>
	</div>
	<div class="overflow-hidden">
		{#each reviews as review, i}
			<div class="review-group relative  pl-10 py-2">
				<img
					src="/svg/quote.svg"
					alt="quote icon"
					class="quote-icon absolute -m-3 h-14"
				/>
				<div
					class="review-card m-2 grid grid-cols-10 items-center rounded-3xl p-4 shadow-lg md:w-[450px] md:gap-5 border"
					style="min-height: 100px;"
					on:mouseenter={event => handleMouseEnter(event, i)}
					on:mouseleave={event => handleMouseLeave(event, i)}
					role="region"
				>
					<img
						src={review.src}
						class="col-span-3 h-28 w-16 rounded-full object-cover md:h-40 md:w-20"
						alt="reviewer_image"
					/>
					<div class="col-span-7">
						<p class="text-gray-600">"{review.review}"</p>
					</div>
				</div>
			</div>
		{/each}
	</div>
</div>

<style>
	.review-card {
		transition: box-shadow 0.3s;
		will-change: transform;
	}
</style>
