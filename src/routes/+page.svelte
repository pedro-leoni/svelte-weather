<script>
	const apiKey = '4ae2636d8dfbdc3044bede63951a019b';
	// estas declaraciones funcionan como estados, la que tiene el export indica que la voy a usar en el html como una prop
	let ciudad = '';
	export let info = [];
	let loading = false;
	let search = null;
	// declaracion reactiva, el html estara escuchando cada vez que se ejecute y por ende cambie la info 
	// es como el useEffect 
	$:if(search){
		fetch(`http://api.openweathermap.org/data/2.5/weather?q=${ciudad}&appid=${apiKey}&units=metric`)
			.then((r) => r.json())
			.then((r) => {
				if(r.cod === 200){
					let find = null;
					info.find((c)=>{
						if(c.r.id === r.id){
							return find = true
						} else {
							return find = false
						}
					})
					if(find){
						alert('Esta ciudad ya se encuentra en la lista')
					} else {
						info.push({ r })
					}
				} else {
					alert('Ciudad no encontrada')
				}
			})
			.then(()=> loading = false)
	}
	// handlers 
	const handleClick = (e) => {
		e.preventDefault();
		search = true 
		loading = true
		setTimeout(() => {
			search = false
		}, 500);
	}
	const handleChange = (e) => {
		ciudad = e.target.value;
	};
	const consolePutoLog = (e) => {
		e.preventDefault();
		console.log(info);
	};
</script>


	<h1>Wheather App</h1>
	<input type="text" name="city" id="city" value={ciudad} on:change={handleChange} />
	<button on:click={handleClick}> search </button>
	<button on:click={consolePutoLog}> ver info en consola </button>
	<div>
		<!-- Renderizado condicional -->
        {#if loading}
		<p>Loading...</p>
		{:else}
			{#if info.length}
				<p>{info.length} Ciudades en la lista</p>
			{:else} 
				<p>Debes buscar una ciudad para ver su informacion climatica</p>
			{/if}
		{/if}
    </div>
