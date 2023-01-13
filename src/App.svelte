<script lang="ts">
    import { onMount } from "svelte";


    let perClick = 1
    let memeCoins = 0

    onMount(() => {
        document.getElementById("")
    })

</script>

<main>
    <h1 id="title">meme clicker</h1>
    <div id="container">
        <b-x>
            <h1>Click the meme</h1>
            <h2>you have {memeCoins} memecoins</h2>
            <h3>Each click gives: 1 memecoin</h3> 
            <img id="meme" width="50" height="50" src="https://i1.sndcdn.com/avatars-qrMzS7F9pCkmuP6Q-KbCIKA-t240x240.jpg" alt="click"/>
        </b-x>
        <b-x>
            <h1>Buy memes</h1>
            <upgrade>
                <h1>Doge Meme</h1>
                <h2>+1 Click</h2>
                <img class="upgrade" width="50" height="50" src="https://www.exodus.com/img/news/content/2022/11/flat-550x550-075-f.u1.jpg" alt="click"/>
            </upgrade>
            
        </b-x>
    </div>
</main>