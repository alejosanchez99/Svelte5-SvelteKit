<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	import { AlarmCheck, Search } from 'lucide-svelte';
</script>

<!-- <h1>Outer</h1>
<DisplayName /> -->
<!-- <RandomNumber /> -->
<!-- <Counter /> -->

<div class="wrapper">
	<Button size="sm" bgColor="green" textColor="yellow">
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

<style>
	:global {
		body {
			background: #222;
		}
	}
	.wrapper :global {
		button {
			background-color: blue;
		}
	}

	/* :global(body) {
		background-color: #222;
	} 
	.wrapper :global(button) {
		background-color: blue;
	} */
</style>
