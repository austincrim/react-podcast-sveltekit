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


<h1>Episodes</h1>
<main>
  {#each episodes as ep}
    <button on:click={() => $episode = ep}>{ep.title}</button>
  {/each}
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    gap: 2rem;
  }
</style>