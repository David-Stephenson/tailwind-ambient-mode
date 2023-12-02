<script>
	import { onMount } from 'svelte';

	let video; // <video> element
	let canvas; // <canvas> element

	onMount(() => {
		const ctx = canvas.getContext('2d');

		// Draw the video to the canvas every 50ms
		video.addEventListener(
			'play',
			function () {
				const draw = function () {
					if (video.paused || video.ended) return;
					ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
					setTimeout(draw, 50);
				};
				draw();
			},
			false
		);
	});
</script>

<div class="flex flex-col items-center justify-center h-screen relative overflow-hidden">
	<!-- Background glow canvas -->
	<canvas bind:this={canvas} class="aspect-video h-[34rem] absolute blur-[200px]" aria-hidden="true"
	></canvas>

	<!-- 
        Le Tailwind definitions:
        aspect-video: 16:9 aspect ratio
        h-[34rem]: 34rem height
        absolute: position absolute to parent
        blur-[100px]: 100px blur
        aria-hidden="true": hide from screen readers
     -->

	<!-- Video element -->
	<video
		bind:this={video}
		class="aspect-video h-[30rem] relative border-4 border-white rounded-md"
		src="https://data.davidstephenson.net/Hero/vein-1280x720/video.m4v"
		controls
		muted
		loop
	></video>

	<!-- 
        Le Tailwind definitions:
        aspect-video: 16:9 aspect ratio
        h-[30rem]: 30rem height
        relative: position relative to parent
        border-4: 4px border
        border-white: white border
        rounded-md: medium rounded corners
     -->

	<div class="fixed bottom-0 right-0">
		<p class="text-white text-right">Video: Beeple - GLASS VEIN</p>
	</div>
</div>
