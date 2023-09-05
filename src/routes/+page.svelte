<script lang="ts">
	import { Marquee } from '$lib/marquee';
</script>

<p>Welcome to demo of a custom marquee/ticker component</p>
<p>Resize the window to try out its responsivity</p>
<Marquee>
	<div class:marquee-item={true}>
		<span>Item 1</span>
	</div>
	<div class:marquee-item={true}>
		<span>Item 2</span>
	</div>
	<div class:marquee-item={true}>
		<span>Item 3</span>
	</div>
	<div class:marquee-item={true}>
		<span>Item 4</span>
	</div>
	<div class:marquee-item={true}>
		<span>Item 5</span>
	</div>
</Marquee>
<a href="https://github.com/bartosjiri/svelte-marquee-demo" target="_blank">Source code</a>
<a href="https://twitter.com/bartosjiri_/status/1698985341951058410" target="_blank">Guide</a>

<style lang="scss">
	:global(.marquee-container) {
		width: 80vw;
		margin: 1.2rem 0;

		.marquee-item {
			display: flex;
			margin: 0 1.6rem;

			span {
				white-space: pre;
			}
		}
	}
</style>
