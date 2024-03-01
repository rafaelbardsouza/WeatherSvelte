<script>
	let WeatherApp = false
	function landing(){
		WeatherApp = false
	}
	let inputText,location,degrees,rain = ""
	async function fetchData() {
		WeatherApp = true
		const url = `https://api.tomorrow.io/v4/weather/realtime?location=${inputText}&apikey=V50ig59AvXny8LFCm8d5bwqto7jZDYjJ`
		try{
			const response = await fetch(url)
			const data = await response.json()
			location = data.location.name
			degrees = data.data.values.temperature+"°C"
			rain = "Rain probablity: "+data.data.values.precipitationProbability+"%"
		} catch (error){
			console.error(error)
		}
	}
</script>

<main>
	<button on:click={landing}>Weather Svelte</button>
	<input bind:value={inputText}/>
	<button on:click= {fetchData}>Search</button>
	{#if WeatherApp}
		<p>{location}</p>
		<p>{degrees}</p>
		<p>{rain}</p>
	{:else}
	<body>
		<h2>Welcome to Svelte Weather app!</h2>
		<p>Explore the weather by searching for a city.</p>
		<p>Example Data:</p>
		<ul>
		  <li>City: New York</li>
		  <li>Temperature: 25°C</li>
		  <li>Rain Probability: 20%</li>
		</ul>
	</body>
	{/if}
</main>

<style>

</style>
