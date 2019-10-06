<script>
import { onMount } from "svelte"; // Importamos onMount un método que utilizaremos para detectar cuándo esta montado el componente.

// Creamos una constate API con la URL de la API publica
const API = "https://rickandmortyapi.com/api/character";

// Asignamos la variable "data" y "characters" como arreglos vacíos.
let data = [];
let characters = [];

// Utilizamos el método onMount para crear lógica una vez que se haya montado en el DOM el componente
onMount(async () => {
// Creamos un llamado a la API por medio de Fetch
const res = await fetch(API);
// Utilizamos "data" para asignar el resultado de la llamada
data = await res.json();
// Cargamos a characters el resultado de los personajes
characters = data.results;
});
</script>

<div class="characters">

  {#each characters as character}
    <figure>
      <img src={character.image} alt={character.name} />
      <figcaption>{character.name}</figcaption>
    </figure>
  {:else}
    <p>loading...</p>
  {/each}

</div>

<style>
.characters {
    width: 100%;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-gap: 8px;
    margin-top: 20px;
}
figure,
img {
    width: 100%;
    margin: 0;
    font-size: 12px;
}
</style>