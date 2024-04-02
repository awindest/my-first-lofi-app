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


<h1>Universal Count: <div class="number">{app_state.counter}</div></h1>

<button {onclick}>Click</button>

<button {onclickReset}>Reset</button>


<p>
	Websocket connection status: {connected ? '🟢 - Yes' : '🔴 - No'}
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
	.number {
		font-family: 'Inter', sans-serif;
		font-feature-settings: 'zero', 'tnum';
  /* 'zero' => adds a slash to a zero to distinguish from an 'O' */
  /* 'tnum' => change variable-spaced numbers to mono-spaced for formatting */
	}
</style>
