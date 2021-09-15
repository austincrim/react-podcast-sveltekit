<script context="module">
  export const load = async ({ page, fetch }) => {
		const response = await fetch(`https://api.simplecast.com/podcasts/bdb43d4d-bd1d-4fbc-bd60-40f1e3299aa3/episodes?status=published&limit=1&type=full,bonus&search=${page.params.slug}`)
    const data = await response.json()
    
    return {
      props: {
        episode: data.collection[0]
      }
    }
    
  }
</script>

<script>
  export let episode
  
  import { episode as episodeStore } from '$lib/store'
</script>

<main>
  <h1>{episode.title}</h1>
  <p>{episode.description}</p>
  <button on:click={() => $episodeStore = episode}>Play</button>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-block: 4rem;
    max-width: 75%;
    margin: 0 auto;
  }
  p {
    max-width: 80ch;
  }
</style>