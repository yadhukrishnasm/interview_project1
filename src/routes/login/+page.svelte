<script>
	import gsap from 'gsap';
	import { onMount } from 'svelte';

	let images = [
		'/images/3.jpg',
		'/images/4.jpg',
		'/images/5.jpg',
		'/images/6.jpg',
		'/images/7.jpg',
		'/images/8.jpg',
		'/images/9.jpg',
		'/images/10.jpg',
		'/images/12.jpg',
		'/images/14.jpg',
		'/images/13.jpg',
		'/images/15.jpg',
		'/images/16.jpg',
		'/images/17.jpg',
		'/images/18.jpg',
		'/images/19.jpg',
		'/images/20.jpg',
		'/images/21.jpg',
		'/images/22.jpg'
	];

	let minDistance = 10;
	let positions = [];
	let containerOffset = { x: 0, y: 0 };

	for (let i = 0; i < images.length; i++) {
		let tries = 0;
		while (true) {
			let top = Math.random() * 100;
			let left = Math.random() * 100;
			if (top > 40 && top < 60 && left > 50 && left < 50) continue;
			let tooClose = positions.some((pos) => {
				let dx = pos.left - left;
				let dy = pos.top - top;
				return Math.sqrt(dx * dx + dy * dy) < minDistance;
			});
			if (!tooClose) {
				positions.push({ top, left });
				break;
			}
			tries++;
			if (tries > 100) {
				positions.push({ top, left });
				break;
			}
		}
	}

	onMount(() => {
		const isSmallDevice = window.innerWidth <= 640;
		 gsap.to(
			'.image-box',
			{
				opacity: 1,
				duration: 1.2,
				ease: 'power2.in',
				stagger: 0.1
			},
			'+=0.1'
		);
	});

	function handleMouseMove(event) {
		const widthCenter = window.innerWidth / 2;
		const heightCenter = window.innerHeight / 2;
		const mouseX = event.clientX;
		const mouseY = event.clientY;
		containerOffset = {
			x: (widthCenter - mouseX) / 10,
			y: (heightCenter - mouseY) / 10
		};
	}

	onMount(() => {
		window.addEventListener('mousemove', handleMouseMove);
		return () => window.removeEventListener('mousemove', handleMouseMove);
	});
</script>

<div class="flex h-screen items-center bg-[#f9eae1]">

	<form class="flex z-10 bg-[#f9eae1] h-full w-[60vw] flex-col justify-center space-y-6 border p-10 shadow-md">
		<h2 class="font-instrument text-center text-6xl">Login</h2>
		<div>
			<label class="font-libre mb-1 block text-gray-700" for="email">Email</label>
			<input
				id="email"
				type="email"
				class="w-full rounded-lg border border-gray-300 bg-neutral-50 px-3 py-2 focus:ring-2 focus:ring-blue-500 focus:outline-none"
				placeholder="Enter your email"
				required
			/>
		</div>
		<div>
			<label class="font-libre mb-1 block text-gray-700" for="password">Password</label>
			<input
				id="password"
				type="password"
				class="w-full rounded-lg border border-gray-300 bg-neutral-50 px-3 py-2 focus:ring-2 focus:ring-blue-500 focus:outline-none"
				placeholder="Enter your password"
				required
			/>
		</div>
		<button
			type="submit"
			class="font-kalnia w-full rounded-xl bg-red-500 py-2 text-white transition hover:bg-blue-700"
		>
			Login
		</button>
	</form>

    	<div
		class="canvas-container  md:-mt-10 md:-ml-20"
		role="region"
		style="width: 130vw; height: 110vh; transform: translate({containerOffset.x}px, {containerOffset.y}px); transition: transform .3s linear; "
	>
		<div>
			{#each images as img, i}
				<div class="image-box" style="top: {positions[i].top}%; left: {positions[i].left}%;">
					<img src={img} alt="Paper Piece" />
				</div>
			{/each}
		</div>
	</div>
</div>

<style>
	.canvas-container {
		position: relative;
		width: 100vw;
		height: 100vh;
        z-index: 1; 
		overflow: hidden;
	}

	.image-box {
		position: absolute;
		display: flex;
		height: 15%;
		align-items: center;
		justify-content: center;
		opacity: 0; /* Initial state for GSAP */
		transition: all ease-in-out 2s;
	}
	.image-box img {
		width: 90%;
		height: 90%;
		object-fit: cover;
	}
</style>
