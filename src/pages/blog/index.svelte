<script context="module" lang="ts">
  const allPosts = import.meta.glob('./*.{md,svx}');
  const postData = [];
  for (let path in allPosts) {
    console.log(path);
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
  $: console.log(posts);
</script>

<div>
  <h1>blog</h1>
  <ul>
    {#each posts as { path, metadata: { title, tags } }}
      <li>
        <a href={`/blog/${path.replace('.md', '').replace('.svx', '')}`}>{title}</a>
        <p>{title}</p>
        <p>{path}</p>
      </li>
    {/each}
  </ul>
</div>

<style>
  p {
    color: #ff3e00;
  }
</style>
