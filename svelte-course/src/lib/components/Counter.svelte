<script lang="ts">
	let count = $state(0);
	let frequency = $state(1000);
	let paused = $state(false);

	$effect(() => {
		let interval: ReturnType<typeof setInterval>;
		if (!paused) {
			interval = setInterval(() => {
				count += 1;
			}, frequency);
		}
		return () => {
			clearInterval(interval);
		};
	});
</script>

<h1>{count}</h1>
{frequency}

<button
	onclick={() => {
		count = 0;
        const originalFrequency = frequency;
        frequency = 0;
        frequency = originalFrequency;
	}}>Reset</button
>
<button onclick={() => (paused = !paused)}>{paused ? 'Play' : 'Pause'}</button>

<button
	onclick={() => {
		frequency *= 2;
	}}>Slower</button
>
<button
	onclick={() => {
		frequency /= 2;
	}}>Faster</button
>
