<script>
	import { app_state, yCounter } from '$lib/all_stores.svelte';

	let connected = $state(false);
	const socket = new WebSocket('ws://localhost:1234');

	// Just to toggle the red green status emoji
	socket?.addEventListener('open', () => (connected = true));
	socket?.addEventListener('close', () => (connected = false));

	// Tells YJS to update the counter
	// This then updates the svelte state and updates the UI
	function onclick() {
		yCounter.set('value', app_state.counter + 1);
	}
	function onclickReset() {
		app_state.counter = 0
		yCounter.set('value', app_state.counter);
	}
</script>
<div class="container">
	<div class="block">


<h1>Universal Count: {app_state.counter}</h1>

<button {onclick}>Click</button>

<button {onclickReset}>Reset</button>


<p>
	Websocket connection status: {connected ? '🟢' : '🔴'}
</p>
</div>
</div>

<style>
	h1, p, button {
		font-family: 'Averox'	
	}
	.container {
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.block {
		display: block;
	}
</style>
