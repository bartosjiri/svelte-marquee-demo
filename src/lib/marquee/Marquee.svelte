<script lang="ts">
	import { onMount } from 'svelte';

	export let speed = 50;

	let containerWidth: number;
	let marqueeRef: HTMLElement;
	let listRef: HTMLElement;

	let listWidth = 0;
	let duration = 0;

	const setupMarquee = () => {
		if (!marqueeRef || !listRef) return;

		Array.from(marqueeRef.children).forEach((child) => {
			if (child != listRef) {
				marqueeRef.removeChild(child);
			}
		});

		listWidth = listRef.offsetWidth || 1;
		duration = listWidth / speed;

		const clonesCount = Math.ceil(containerWidth / listWidth);
		for (let i = 0; i < clonesCount; i++) {
			const clone = listRef.cloneNode(true);
			if (!clone) return;
			marqueeRef.appendChild(clone);
		}

		marqueeRef.style?.setProperty('animation-play-state', 'paused');
		setTimeout(() => {
			marqueeRef.style?.setProperty('animation-play-state', 'running');
		}, 10);
	};

	onMount(() => {
		setupMarquee();
	});
</script>

<svelte:window on:resize={setupMarquee} />
<div bind:clientWidth={containerWidth} class:marquee-container={true}>
	<div
		bind:this={marqueeRef}
		class:marquee={true}
		style="
			--offset: {listWidth}px;
			--duration: {duration}s;
		"
	>
		<div bind:this={listRef} class:list={true}>
			<slot />
		</div>
	</div>
</div>

<style lang="scss">
	.marquee-container {
		position: relative;
		overflow: hidden;

		&:before,
		&:after {
			position: absolute;
			content: '';
			top: 0;
			bottom: 0;
			width: 2.4rem;
			z-index: 1;
		}

		&:before {
			left: 0;
			background: linear-gradient(to right, #fff, transparent);
		}

		&:after {
			right: 0;
			background: linear-gradient(to left, #fff, transparent);
		}

		.marquee {
			display: flex;
			justify-content: flex-start;
			animation-name: marqueeScroll;
			animation-duration: var(--duration);
			animation-timing-function: linear;
			animation-iteration-count: infinite;
			animation-play-state: running;
			will-change: transform;

			@keyframes marqueeScroll {
				0% {
					transform: translate3d(0, 0, 0);
				}

				100% {
					transform: translate3d(calc(var(--offset) * -1), 0, 0);
				}
			}

			.list {
				display: flex;
			}
		}
	}
</style>
