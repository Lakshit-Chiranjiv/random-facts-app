<script>
  import { onMount } from "svelte";
  import axios from "axios";

  let fact = "";

  const getRandomFact = async () => {
    console.log(import.meta.env.VITE_API_KEY);
    fact = "Loading...";
    const response = await axios.get("https://api.api-ninjas.com/v1/facts", {
      headers: {
        'X-Api-Key': import.meta.env.VITE_API_KEY
      }
    });
    fact = response.data[0].fact;
  };

  onMount(() => {
    getRandomFact();
  });
</script>

<main>
  <h1>Random Facts Generator</h1>
  <p>{fact}</p>
  <button on:click={getRandomFact}>Generate Random Fact</button>
</main>

<style>
  main {
    text-align: center;
    padding: 2rem;
  }

  h1 {
    font-size: 2rem;
    margin-bottom: 1rem;
  }

  p {
    margin-bottom: 1rem;
  }

  button {
    padding: 0.5rem 1rem;
    font-size: 1rem;
  }

  @media screen and (max-width: 620px) {
    h1 {
      font-size: 1.5rem;
    }

    p {
      font-size: 1rem;
    }

    button {
      font-size: 0.75rem;
    }
  }

</style>
