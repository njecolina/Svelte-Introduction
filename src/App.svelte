<script>
	import {fade, fly} from 'svelte/transition';

	export let name;

	let rando;

	$: result = Math.round(rando * 100);

	function setRando(){
		rando = Math.random();
	}
</script>

<main>
	<h1>Hello {name}!</h1>
	<hr>
	<p>The random number is:</p>
	<p>{rando}</p>
	<hr>
	<p>{result}</p>
	<button on:click={setRando}>Randomize</button>
	{#if result > 75}
		<p 
		in:fly={{x: 1000, duration: 200}}
		out:fly={{x: -1000, duration: 200}}>
			Big winning! Top 25%!
		</p>
	{:else if result > 50}
		<p transition:fly>Good enough! In top 50%!</p>
	{:else}
		<p transition:fade>Not good enough number, sorry!</p>
	{/if}
	<p>Your name:</p>
	<input bind:value={name}>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>