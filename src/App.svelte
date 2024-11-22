<script lang="ts">
  import { onMount } from 'svelte';
  import { fetchArtworks } from './lib/api';

  let artwork: { id: string, title: string; description: string; url: string }[] = [];
  let error = '';

  onMount(async () => {
    try {
      artwork = await fetchArtworks();
    } catch (err) {
      error = 'Failed to fetch artworks';
    }
  });
</script>

<style>
  .pictures {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
  }
  .picture {
    text-align: center;
  }
  img {
    max-width: 100%;
    height: auto;
    border-radius: 8px;
  }
</style>

{#if error}
  <p class="error">{error}</p>
{/if}

<div class="pictures">
  {#each artwork as { title, description, url }}
    <div class="picture">
      <img src={url} alt={title} />
      <h3>{title}</h3>
      <p>{description}</p>
    </div>
  {/each}
</div>
