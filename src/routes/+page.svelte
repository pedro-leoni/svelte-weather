<script>
	const apiKey = '4ae2636d8dfbdc3044bede63951a019b';
	let ciudad = '';
	const info = [];
	const searchCity = (e) => {
		e.preventDefault();
		fetch(`http://api.openweathermap.org/data/2.5/weather?q=${ciudad}&appid=${apiKey}&units=metric`)
			.then((r) => r.json())
			.then((r) => info.push({ r }));
	};
	const handleChange = (e) => {
		ciudad = e.target.value;
	};
	const consolePutoLog = (e) => {
		e.preventDefault();
		console.log(info);
	};
</script>

<main>
	<h1>Wheather App</h1>
	<form on:submit={searchCity}>
		<input type="text" name="city" id="city" on:change={handleChange} />
		<button type="submit"> buscar </button>
	</form>
	<button on:click={consolePutoLog}> ver info en consola </button>
	<div>
        <h2>Ciudades</h2>
        
    </div>
</main>
