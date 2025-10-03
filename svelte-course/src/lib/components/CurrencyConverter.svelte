<script lang="ts">
	import dummyRates from '$lib/utils/dummy-rates';

	let baseValue = $state(1);
	let baseCurrency = $state('usd');
	let baseRates = $derived(dummyRates[baseCurrency]);
	let targetCurrency = $state('eur');
	let targetValue = $derived(
		baseValue && baseRates[targetCurrency] && baseValue * baseRates[targetCurrency]
	);
</script>

<div class="wrapper">
	<div class="conversion">
		<span class="base"
			>{Number(1).toLocaleString('en-US', {
				style: 'currency',
				currency: baseCurrency,
				currencyDisplay: 'name'
			})} equals</span
		>
		<span class="target"
			>{baseRates[targetCurrency].toLocaleString('en-US', {
				style: 'currency',
				currency: targetCurrency,
				currencyDisplay: 'name'
			})}</span
		>
	</div>
	<div class="base">
		<input
			type="number"
			bind:value={
				() => baseValue,
				(value) => {
					baseValue = baseValue < 0 ? 1 : value;
				}
			}
		/>

		<select bind:value={baseCurrency}>
			<option value="usd">United States Dollar</option>
			<option value="eur">Euro</option>
			<option value="gbp">Pound Sterling</option>
		</select>
	</div>
	<div class="target">
		<input type="number" bind:value={targetValue} />
		<select bind:value={targetCurrency}>
			<option value="usd">United States Dollar</option>
			<option value="eur">Euro</option>
			<option value="gbp">Pound Sterling</option>
		</select>
	</div>
</div>

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
	.wrapper {
		font-family: Arial, Helvetica, sans-serif;
		background-color: #131313;
		padding: 20px;
		margin: 20px 10px;
		border-radius: 10px;
		.conversion {
			margin-bottom: 20px;
			color: white;

			span.base {
				opacity: 0.6;
				font-size: 14px;
				display: block;
				margin-bottom: 5px;
			}
			span.target {
				font-size: 28px;
				display: block;
			}
		}
		.base {
			margin-bottom: 15px;
		}
		.base,
		.target {
			select,
			input {
				background-color: transparent;
				color: #fff;
				border: 1px solid rgba(255, 255, 255, 0.1);
				border-radius: 5px;
				padding: 10px;
				&:focus-visible {
					outline: 1px solid rgb(65, 189, 209);
				}
			}
			input {
				&::-webkit-outer-spin-button,
				&::-webkit-inner-spin-button {
					-webkit-appearance: none;
					margin: 0;
				}
			}
		}
	}
</style>
