<script>
	let showResult = false
	let gayProbability = Promise.resolve(1)
	let gPressed = false

	let gPress = () => {
		console.log("Dragged")
		setTimeout(()=>{
			gPressed = false
			console.log("Done")
		}, 5000)
		gPressed = true
	}

	let testGay = () => {
		showResult = true
		gayProbability = new Promise((resolve, reject) => {
			setTimeout(() => {
				let percent = 0
				if(gPressed){
					percent = 0 + (Math.random() * 10) // 0 + (0 - 10)
				} else{
					percent = 100 - (Math.random() * 20)
				}
				resolve(percent)
			}, 1500 + (Math.random() * 500)) // 1500 + (0 - 500)
		})
	}

	let clearGay = () => {
		showResult = false
		testGay();
	}
</script>

<h1>Gaydar</h1>
<h3>The most accurate gaydar on the internet!</h3>
{#if showResult}
	{#await gayProbability}
		<p>Calculating gayness...</p> <br/>
		<img src="https://media2.giphy.com/media/3oEjI6SIIHBdRxXI40/200.gif" alt="Loading"/><br>
	{:then gayProbabilityResolved} 
		<p>Your gayness is {gayProbabilityResolved.toFixed(2).toString()}%</p>
	{/await}
	<button on:click={clearGay}>Recalculate</button>
{:else}
	<button on:click={testGay}>Test gayness</button>
{/if}

<h6 style="position: absolute; bottom: 0px;" on:dragend={gPress}>Made by Daniel Florescu</h6>