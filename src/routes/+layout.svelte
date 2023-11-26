<script lang="ts">
	import Background from '$lib/Background.svelte';
	import Footer from '$lib/Footer.svelte';
	import Header from '$lib/header/Header.svelte';
	import '../app.css';
</script>

<svelte:head>
	<title>i am RIVAS</title>
</svelte:head>

<Background />
<main>
	<Header />
	<slot />
	<Footer />
</main>

<style>
	main {
		position: relative;
		padding: 1rem;
		width: 100%;
		height: 100vh;
		max-width: 960px;
		margin: 0 auto;
		box-sizing: border-box;
		pointer-events: none;
	}
</style>
