<script>
	import gsap from 'gsap';
	import {onMount} from 'svelte';
	// Array of image URLs (replace with your images)
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
        gsap.from('.center-text', {
            opacity: 0,
            y: 40,
            duration: 1.2,
            ease: 'power2.in'
        });
        gsap.from('.image-box', {
            opacity: 0,
            scale: 0.8,
            rotate: -10,
            duration: 1.2,
            ease: 'power2.in',
            stagger: 0.08,
            delay: 0.2
        });
    });
	let positions = images.map(() => ({
		top: Math.random() * 80 + 5, // 5% to 85%
		left: Math.random() * 80 + 5 // 5% to 85%
	}));
</script>

<div class="canvas-container">
	<div class="center-text">
		<h1>Creating Artworks <br /> That Resonates <br /> Thy self</h1>
		<p>Some description here.</p>
	</div>
	{#each images as img, i}
		<div class="image-box" style="top: {positions[i].top}%; left: {positions[i].left}%;">
			<img src={img} alt="Paper Piece" />
		</div>
	{/each}
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
