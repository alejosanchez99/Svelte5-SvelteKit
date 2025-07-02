<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	import { AlarmCheck, Search } from 'lucide-svelte';

	let html = '<p>test</p>';
	let button: Button;

	$effect(() => {
		button.getButton().focus();
		// button.focus();
	});
</script>

<!-- <h1>Outer</h1>
<DisplayName /> -->
<!-- <RandomNumber /> -->
<!-- <Counter /> -->

<div class="wrapper">
	{@html html}
	<!-- <div
		onclick={() => {
			console.log('event coming from div');
		}}
	> -->
	<Button
		bind:this={button}
		size="lg"
		--buttonBgColor="yellow"
		--buttonTextColor="green"
		onlefthover={() => {
			console.log('object');
		}}
		onclick={(e) => {
			e.stopPropagation();
			console.log('event from buttom');
		}}
	>
		{#snippet left(isHovered: boolean)}
			{#if isHovered}
				<Search />
			{:else}
				<AlarmCheck />
			{/if}
		{/snippet}
		Text
		<!-- {#snippet children(isLeftHovered)}
		Text {isLeftHovered}
	{/snippet} -->
		{#snippet right()}
			<AlarmCheck />
		{/snippet}
	</Button>
</div>

<!-- </div> -->

<style>
	:global {
		body {
			background: #222;
		}
	}
	.wrapper :global {
		/* button {
			background-color: blue;
		} */
		p {
			color: white;
		}
	}

	/* :global(body) {
		background-color: #222;
	} 
	.wrapper :global(button) {
		background-color: blue;
	} */
</style>
