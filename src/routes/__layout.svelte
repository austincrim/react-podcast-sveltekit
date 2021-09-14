<script>
  import {episode} from '$lib/store'
  import { onMount } from 'svelte';
  let player

  onMount(() => {
    return episode.subscribe(() => {
      player.load()
    })
  })
</script>

<nav>
  <a href="/">Home</a>
  <a href="/about">About</a>
</nav>

{#if $episode}
  <div class='player'>
    <p style="font-weight: bold;">{$episode.title}</p>
    <audio bind:this={player} style="margin-bottom: 5rem;" controls>
      <source src={$episode.enclosure_url} type="audio/mpeg">
    </audio>
  </div>
{/if}

<slot/>

<style>
  :global(html) {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }
  nav {
    display: flex;
    justify-content: center;
    gap: 2rem;
    margin-bottom: 2rem;
  }

   .player {
    position: fixed;
    bottom: 0;
    left: 0;
    padding: 0 1rem;
  }
</style>