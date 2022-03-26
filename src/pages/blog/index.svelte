<script context="module" lang="ts">
  const allPosts = import.meta.glob('./*.{md,svx}');
  const postData = [];
  for (let path in allPosts) {
    postData.push(
      allPosts[path]().then(({ metadata }) => {
        return { path, metadata };
      })
    );
  }
  export const load = async () => {
    const posts = await Promise.all(postData);
    return posts;
  };
</script>

<script>
  import { onMount } from 'svelte';
  export let posts = [];
  onMount(async () => {
    posts = await load();
  });
</script>

<div>
  <h1>blog</h1>
  <ul>
    {#each posts as { path, metadata }}
      <li>
        <p>{metadata.title}</p>
      </li>
    {/each}
  </ul>
</div>

<style>
  p {
    color: #ff3e00;
  }
</style>
