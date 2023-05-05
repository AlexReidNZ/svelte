<script>
    const BASE_URL = "https://www.giantbomb.com/api";

    fetch(`${BASE_URL}/games/?api_key=cb638b4d991587308456a3533f0914df1b87309d&format=json&field_list=name`)
    .then(res => {
        console.log(res)
    });
    
</script>

<p>this is the home page.</p>