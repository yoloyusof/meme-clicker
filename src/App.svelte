<script lang="ts">
  import { onMount } from "svelte";

  let desearialized;

  if (localStorage.getItem("data")) {
    desearialized = JSON.parse(localStorage.getItem("data"));
  } else {
    desearialized = { memeCoins: 0, perClick: 1, planet: "Earth" };
  }

  let planetMappings = {
    Earth: 1,
    Ohio: 10,
    MCU: 50,
  };

  let memes = [
    "https://i.ytimg.com/vi/gz0CYLoE6_o/maxresdefault.jpg",
    "https://i.ytimg.com/vi/zRomlhpMeHs/mqdefault.jpg",
    "https://www.exodus.com/img/news/content/2022/11/flat-550x550-075-f.u1.jpg",
  ];

  let perClick = desearialized.perClick;
  let memeCoins = desearialized.memeCoins;
  let planet = desearialized.planet;

  onMount(() => {
    let memeElement = document.getElementById("meme") as HTMLImageElement;
    memeElement.src = memes[Math.floor(Math.random() * memes.length)];
    document.getElementById("meme").onclick = () => {
      let perClickByPlanet;

      if (planet == "Earth") {
        perClickByPlanet = perClick;
      } else if (planet == "Ohio") {
        perClickByPlanet = perClick * planetMappings.Ohio;
      } else if (planet == "MCU") {
        perClickByPlanet = perClick * planetMappings.MCU;
      }

      memeCoins += perClickByPlanet;
      
    };

    document.getElementById("buy-doge").onclick = () => {
      if (memeCoins <= 5) return;
      memeCoins -= 5;
      perClick += 1;
    };

    document.getElementById("buy-ishowspeed").onclick = () => {
      if (memeCoins <= 20) return;
      memeCoins -= 20;
      perClick += 4;
    };

    document.getElementById("travel-ohio").onclick = () => {
      if (planet == "Ohio") return;
      if (memeCoins <= 9000) return;
      planet = "Ohio";

      memeCoins = 0;
      perClick = 1;
    };

    document.getElementById("buy-genzkid").onclick = () => {
      if (memeCoins <= 50) return;
      memeCoins -= 50;
      perClick += 10;
    };

    document.getElementById("travel-mcu").onclick = () => {
      if (planet == "MCU") return;
      if (memeCoins <= 500000) return;
      planet = "MCU";

      memeCoins = 0;
      perClick = 1;
    };

    window.addEventListener("unload", () => {
      localStorage.setItem(
        "data",
        JSON.stringify({
          memeCoins: memeCoins,
          perClick: perClick,
          planet: planet,
        })
      );
    });
  });
</script>

<main>
  <img src="Meme clicker banner.png" alt="banner" id="title" />
  <div id="container">
    <b-x>
      <h1 id="titleText">Click the meme</h1>
      <h2>
        you have <h3 style="color: rgb(99, 239, 99);">{memeCoins}</h3>
        memecoins
      </h2>
      <br />
      <h3>Each click gives: {perClick} memecoin</h3>
      <h3>With a planet multiplier of x{planetMappings[planet]}</h3>
      <img
        id="meme"
        width="50"
        height="50"
        src="https://i1.sndcdn.com/avatars-qrMzS7F9pCkmuP6Q-KbCIKA-t240x240.jpg"
        alt="click"
      />
    </b-x>
    <b-x>
      <h1>Buy memes</h1>
      <h2>Bob's meme shop</h2>
      <upgrade>
        <h1>Doge Meme</h1>
        <h2>+1 Click</h2>
        <h3 class="upgrade-text">Cost: 5 Clicks</h3>
        <img
          class="upgrade"
          width="50"
          height="50"
          src="https://www.exodus.com/img/news/content/2022/11/flat-550x550-075-f.u1.jpg"
          alt="click"
        />
        <br />
        <button id="buy-doge">Buy</button>
      </upgrade>
      <upgrade>
        <h1>IShowSpeed</h1>
        <h2>+4 Click</h2>
        <h3 class="upgrade-text">Cost: 20 Clicks</h3>
        <img
          class="upgrade"
          width="50"
          height="50"
          src="https://i.ytimg.com/vi/zRomlhpMeHs/mqdefault.jpg"
          alt="click"
        />
        <br />
        <button id="buy-ishowspeed">Buy</button>
      </upgrade>
      <upgrade>
        <h1>GENZ Kids</h1>
        <h2>+10 Click</h2>
        <h3 class="upgrade-text">Cost: 50 Clicks</h3>
        <br />
        <button id="buy-genzkid">Buy</button>
      </upgrade>
    </b-x>
    <b-x>
      <h1>Planets</h1>
      <h2>Current Planet: {planet}</h2>
      <h3>Planets reset all your stuff but give you a permanent click boost</h3>
      <upgrade>
        <h1>Ohio</h1>
        <h2>*10 Clicks</h2>
        <h3 class="upgrade-text">Have atleast 9000 memecoins</h3>
        <img
          class="upgrade"
          width="50"
          height="50"
          src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQx0YWwAvMmaFXva-6YJsanNkcqhgiayaJsKSgIBtWQ&s"
          alt="click"
        />
        <br />
        <button id="travel-ohio">Travel</button>
      </upgrade>
      <upgrade>
        <h1>MCU</h1>
        <h2>*50 Clicks</h2>
        <h3 class="upgrade-text">Have atleast 500000 memecoins</h3>
        <img
          class="upgrade"
          width="50"
          height="50"
          src="https://i.ytimg.com/vi/TWB31WFomz4/maxresdefault.jpg"
          alt="click"
        />
        <br />
        <button id="travel-mcu">Travel</button>
      </upgrade>
    </b-x>
  </div>
</main>
