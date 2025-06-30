<script lang="ts">
	import { onDestroy, onMount, tick, untrack } from 'svelte';

	let randomNumber = $state(Math.floor(Math.random() * 10));
	let doubleRandomNumber = $derived(randomNumber * 2);
	let history: number[] = $state([untrack(() => randomNumber)]);
	let historyPTag: HTMLParagraphElement;

	onMount(() => {
		console.log('The component has mounted');

		return () => {
			console.log('The component has unmounted');
		};
	});

	onDestroy(() => {
		console.log('the component is destroyed');
	});

	$effect.pre(() => {
		history.length;
		console.log('$effect.pre', historyPTag?.innerText);
		tick().then(() => {
			console.log('After tick', historyPTag?.innerText);
		});

		return () => console.log('Pre effect Cleanup');
	});

	$effect(() => {
		history.length;
		console.log('$effect', historyPTag.innerText);

		return () => console.log('Effect Cleanup');
	});
</script>

<h2>The random number is : {randomNumber}</h2>
<h2>Double random number is: {doubleRandomNumber}</h2>
<p bind:this={historyPTag}>History {history}</p>
<button
	onclick={() => {
		randomNumber = Math.floor(Math.random() * 10);
		history.push(randomNumber);
	}}
>
	Generate
</button>
