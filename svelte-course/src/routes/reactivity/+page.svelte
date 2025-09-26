<script lang="ts">
	import Notification from '$lib/components/Notification.svelte';
	import Button from '$lib/components/Button.svelte';
	import generateNotifications from '$lib/utils/generate-notifications';

	let notifications = $state.raw(generateNotifications());
</script>

<Button
	onclick={() => {
		notifications = generateNotifications(3);
	}}
	>Refresh
</Button>

<ul>
	{#each notifications as notification, index (notification.id)}
		<li>
			<Notification
				{notification}
				onremove={(id) => {
					notifications = notifications.filter((notification) => notification.id !== id);
				}}
			/>
		</li>
	{/each}
</ul>

<style>
	:global {
		body {
			background-color: #222;
			color: #fff;
		}
	}

	ul {
		list-style: none;
		padding: 10px;
		margin: 0;
		li {
			margin-bottom: 10px;
		}
	}
</style>
