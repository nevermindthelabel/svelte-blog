<script context="module" lang="ts">
  const allPosts = import.meta.glob('./*.{md,svx}');
  let postData = [];
  for (let path in allPosts) {
    postData.push(
      allPosts[path]().then(({ metadata }) => {
        return { path, metadata };
      })
    );
  }
  export const load = async () => {
    const posts = await Promise.all(postData);
    return {
      posts
      // props: {
      //   posts
      // }
    };
  };
</script>

<script>
  import { onMount } from 'svelte';
  export let posts;
  let test;
  onMount(async () => {
    posts = await load();
  });
  console.log(posts);
  console.log(test);
</script>

<div>
  <!-- <p>blog</p> -->
  {JSON.stringify(posts)}
</div>

<style>
  p {
    color: #ff3e00;
  }
</style>
