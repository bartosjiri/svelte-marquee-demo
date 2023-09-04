<script lang="ts">
	import '../styles/_global.scss';
</script>

<main>
	<slot />
</main>

<style lang="scss">
	main {
		height: 100vh;
		width: 100vw;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
</style>
