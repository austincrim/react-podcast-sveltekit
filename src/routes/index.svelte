<script context="module">
  export const prerender = true

  export const load = async ({ fetch }) => {
		const response = await fetch("https://api.simplecast.com/podcasts/bdb43d4d-bd1d-4fbc-bd60-40f1e3299aa3/episodes?status=published&limit=5&type=full,bonus")
		
		let data = await response.json()
		
    return {
      props: {
        episodes: data.collection
      }
    }
  }
</script>

<script>
	export let episodes

  import { episode } from "$lib/store";

  if (!$episode) {
    $episode = episodes[0]
  }
</script>


<main>
  <h1>Episodes</h1>
  {#each episodes as ep}
  <article>
    <a href={`/${ep.slug}`}>{ep.title}</a>
    <button on:click={() => $episode = ep}>Play</button>
  </article>
  {/each}
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    gap: 3rem;
    max-width: 50%;
    margin: 0 auto;
  }

  article {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
</style>