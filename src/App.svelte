<script>
  let name = "afa students";

  let n1 = 9;
  let n2 = 7;

  let listaCompra = [
    "leche",
    "pan",
    "patatas",
    "Papel de aluminio",
    "satélites",
  ];

  let listaCompraFruta = [
    {
      nombre: "fresas",
      emoji: "🍓",
      cantidad: "1Kg",
    },
    { nombre: "kiwis", emoji: "🥝", cantidad: "4uds" },
    { nombre: "naranjas", emoji: "🍊", cantidad: "una malla" },
  ];

  let range = { min: 1, max: 900 };
  let delta = range.max - range.min;

  let pokemon = 448;
  //   let pokemon = Math.round(range.min + Math.random() * delta);
  const URL = `https://pokeapi.co/api/v2/pokemon/${pokemon}`;
  console.log(pokemon);

  const fetchData = (async () => {
    const response = await fetch(URL);
    const data = await response.json();
    return data;
  })();
</script>

<main>
  <h1>Hello {name}!</h1>
  <!-- <p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p> -->

  {#if n1 > n2}
    <p>El primer número es mayor que el segundo</p>
  {:else}
    <p>El primer número es menor que el segundo</p>
  {/if}

  <!-- <h2>mi lista de la compra:</h2>

	<ul>

		{#each listaCompra as cosa}
			<li>{cosa}</li>
		{/each}

	</ul> -->
  <!-- <h2>mi lista de las frutas:</h2> -->

  <!-- <ul>
		{#each listaCompraFruta as fruta}
			<li>{fruta.emoji} {fruta.nombre} x {fruta.cantidad}</li>
		{/each}
	</ul> -->
</main>
<div id="pokemon">
  {#await fetchData}
    <p>...cargando</p>
  {:then data}
    <div class="card">
      <div class="img-container">
        <img src={data.sprites.front_default} alt="imagen de {data.name}" />
      </div>
      <div class="text">
        <h3>{data.name}</h3>
        <ul>
          <li>Altura: {data.height}</li>
          <li>Peso: {data.weight}</li>
        </ul>
      </div>
    </div>
  {:catch error}
    <p>Error:{error}</p>
  {/await}
</div>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }
  ul {
    text-align: left;
    max-width: 200px;
    margin: auto;
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

  #pokemon {
    max-width: 800px;
    margin: auto;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  #pokemon .card {
    display: flex;
    min-width: 300px;
    box-shadow: 0 0 6px rgba(0, 0, 0, 0.3);
    border-radius: 12px;
    padding: 12px;
    gap: 12px;
  }
  #pokemon h3 {
    text-transform: capitalize;
    margin-bottom: 12px;
  }
  #pokemon .img-container {
    width: 80px;
    border: 1px solid gray;
    padding: 8px;
    border-radius: 12px;
    box-sizing: border-box;
    text-align: center;
    display: flex;
    justify-content: center;
  }
  #pokemon img {
    margin: auto;
  }

  #pokemon ul {
    padding-left: 12px;
  }
</style>
