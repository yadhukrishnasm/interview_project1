<script>
	import gsap from 'gsap';
	import { onMount } from 'svelte';

	let images = [
		'/img1.jpg',
		'/img2.jpg',
		'/img3.jpg',
		'/img4.jpg',
		'/img5.jpg',
		'/img6.jpg',
		'/img7.jpg',
		'/img8.jpg',
		'/img9.jpg',
		'/img10.jpg'
	];

	onMount(() => {
		gsap.to('.center-text', {
			y: -40,
			opacity: 1,
			duration: 1.2,
			ease: 'power2.in'
		});
		gsap.to('.image-box', {
			opacity: 1,
			duration: 1.2,
			ease: 'power2.in'
		});
	});

	let minDistance = 18;
	let positions = [];
	let offsets = Array(images.length).fill({ x: 0, y: 0 });

	for (let i = 0; i < images.length; i++) {
		let tries = 0;
		while (true) {
			let top = Math.random() * 80 + 5;
			let left = Math.random() * 80 + 5;
			if (top > 35 && top < 65 && left > 35 && left < 65) continue;
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
			if (tries > 50) {
				positions.push({ top, left });
				break;
			}
		}
	}

	function handleMouseMove(event) {
		const widthCenter = window.innerWidth / 2;
		const heightCenter = window.innerHeight / 2;
		const mouseX = event.clientX;
		const mouseY = event.clientY;

		offsets = positions.map((pos) => {
			// Calculate image center in px
			const imgX = (pos.left / 100) * window.innerWidth;
			const imgY = (pos.top / 100) * window.innerHeight;
			// Use your xY logic, but invert direction for "opposite"
			const resX = -((mouseX - imgX) / 18); // adjust divisor for effect strength
			const resY = -((mouseY - imgY) / 18);
			return { x: resX, y: resY };
		});
	}
</script>

<div class="canvas-container" >
	<div class="center-text opacity-0">
		<h1>Creating Artworks <br /> That Resonates <br /> Thy self</h1>
		<p>Some description here.</p>
	</div>
	<div role="region"  on:mousemove={handleMouseMove}>
		{#each images as img, i}
			<div
				class="image-box"
				style="top: {positions[i].top}%; left: {positions[i].left}%; transform: translate({offsets[
					i
				]?.x || 0}px, {offsets[i]?.y ||
					0}px); transition: transform 0.2s cubic-bezier(.4,0,.2,1); opacity: 0;"
			>
				<img src={img} alt="Paper Piece" />
			</div>
		{/each}
	</div>
</div>

<style>
	.canvas-container {
		position: relative;
		width: 100vw;
		height: 100vh;
		background: #f5f5f5;
		overflow: hidden;
	}

	.center-text {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		z-index: 2;
		text-align: center;
	}
	.image-box {
		position: absolute;
		width: 100px;
		height: 100px;
		z-index: 1;
		border: black solid 1px;
		display: flex;
		align-items: center;
		transition: all ease-in-out 2s;
		justify-content: center;
	}
	.image-box img {
		width: 90%;
		height: 90%;
		object-fit: cover;
	}
</style>
