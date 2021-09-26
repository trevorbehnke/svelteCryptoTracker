<script>
	import '../global.css';
	import { onMount } from 'svelte';
	import CoinCard from '../components/CoinCard.svelte';
	let coins = [];

	const fetchCoins = async () => {
		const response = await fetch('https://api.coinstats.app/public/v1/coins?skip=0&limit=20');
		console.log(response);
		const data = await response.json();
		console.log(data);
		coins = data.coins;
		console.log('coins:', coins);
	};

	onMount(fetchCoins);
</script>

<main>
	<h1>Crypto Tracker</h1>
	<div class="grid">
		{#each coins as coin}
			<CoinCard {coin} />
		{/each}
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 40px 0;
		margin: 0 auto;
	}
	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
		padding-bottom: 3rem;
	}
	.grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
		gap: 30px;
	}
	@media (min-width: 640px) {
		main {
			max-width: 1600px;
			padding: 40px 20px;
		}
	}
</style>
