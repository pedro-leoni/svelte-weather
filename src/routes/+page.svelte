<script>
    const apiKey = '4ae2636d8dfbdc3044bede63951a019b'
    let ciudad = ''
    const searchCity = () => {
        console.log('ciudad', ciudad)
    }
    const handleChange = (e) => {
        ciudad += e.target.value
    }
    fetch(`http://api.openweathermap.org/data/2.5/weather?q=${ciudad}&appid=${apiKey}&units=metric`)
    .then( r => r.json())
    .then( r => console.log(r))
</script>

<main>
   <h1>Wheather App</h1>
   <form on:submit={searchCity}>
    <input type="text" name="city" id="city">
    <button type="submit"> buscar </button>
   </form>
</main>
