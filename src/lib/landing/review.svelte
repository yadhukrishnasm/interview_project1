<script>
    import { onMount } from 'svelte';

    const reviews = [
        { name: 'John Doe', review: 'This is an amazing product! I love it.', rating: 5, src:"/images/p1.jpg" },
        { name: 'Jane Smith', review: 'Great quality and fast shipping.', rating: 4 ,src:"/images/p2.jpg"},
        { name: 'Alice Johnson', review: 'Exceeded my expectations, will buy again!', rating: 5,src:"/images/p3.jpg" },
        { name: 'Alice Johnson', review: 'Exceeded my expectations, will buy again!', rating: 5, src:"/images/p4.jpg" },
        { name: 'Alice Johnson', review: 'Exceeded my expectations, will buy again!', rating: 5,src:"/images/p5.jpg" },
        { name: 'Alice Johnson', review: 'Exceeded my expectations, will buy again!', rating: 5, src:"/images/p6.jpg" },
        { name: 'Bob Brown', review: 'Good value for money, but could improve customer service.', rating: 3,src:"/images/p7.jpg" }
    ];

    let gsap;
    onMount(async () => {
        gsap = (await import('gsap')).default;
    });

    function handleMouseEnter(event) {
        gsap.to(event.currentTarget, {
            x: 40,
            scale: 1.04,
            boxShadow: "0 8px 24px rgba(0,0,0,0.18)",
            duration: 0.5,
            ease: "power2.out"
        });
    }

    function handleMouseLeave(event) {
        gsap.to(event.currentTarget, {
            x: 0,
            scale: 1,
            boxShadow: "0 2px 8px rgba(0,0,0,0.08)",
            duration: 0.5,
            ease: "power2.inOut"
        });
    }
</script>

<div id="review-containter" class="grid h-full grid-cols-2 items-center justify-center">
    <div class="flex flex-col p-20">
        <p class="text-3xl">What Our <br /> Customers Say</p>
        <p>
            Lorem, ipsum dolor sit amet consectetur adipisicing elit. Vitae delectus impedit illum, ex
            repellat dolores voluptatum placeat, mollitia dicta obcaecati reprehenderit commodi fuga
            facere veritatis reiciendis culpa consectetur sequi animi.
        </p>
    </div>
    <div class="overflow-hidden" >
        <div class="marquee-vertical">
            {#each reviews.concat(reviews) as review}
                <div
                    class="review-card m-2 grid grid-cols-10 w-[450px] items-center rounded-lg  p-4 shadow-lg gap-5"
                    style="min-height: 100px;"
                    on:mouseenter={handleMouseEnter}
                    on:mouseleave={handleMouseLeave}
                    role="region"
                >
                    <img src={review.src} class="w-20 h-20 object-cover rounded-full  col-span-3" alt="" />
                    <div class="col-span-7">
                        <p class="text-gray-600">"{review.review}"</p>
                    </div>
                </div>
            {/each}
        </div>
    </div>
</div>

<style>
.marquee-vertical {
  animation: marquee-vert 10s linear infinite;
}
@keyframes marquee-vert {
  0% { transform: translateY(0); }
  100% { transform: translateY(-20%); }
}
.marquee-vertical:hover{
    animation-play-state: paused; /* Pause on hover */
}
.review-card {
    transition: box-shadow 0.3s;
    will-change: transform;
}
</style>