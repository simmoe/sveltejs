<script>
	import { onMount } from 'svelte';
	let name = 'WORLD'
	let mqttMessage = 'waiting..'
	
	const loaded = () => {
		const client = mqtt.connect('wss://mqtt.nextservices.dk') 
		client.subscribe("mqtt/demo")
		client.on("message", (topic, message) => {
			mqttMessage = message			
		})

		client.publish("mqtt/demo", "hello world!")
	}

</script>

<svelte:head>
	<script on:load={loaded} src="https://cdnjs.cloudflare.com/ajax/libs/mqtt/4.3.7/mqtt.min.js" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
</svelte:head>

<main>
	<h1>Hello {name}!</h1>
	<p>Received the following MQTT message: {mqttMessage}</p>
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