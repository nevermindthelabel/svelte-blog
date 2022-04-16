<script context="module" lang="ts">
  const allPosts = import.meta.glob('./blog/*.{md,svx}');
  const postData = [];
  for (let path in allPosts) {
    postData.push(
      allPosts[path]().then(({ metadata }) => {
        return { path, metadata };
      })
    );
  }
  export const load = async () => {
    const posts = await (await Promise.all(postData)).splice(0, 3);
    return posts;
  };
</script>

<script lang="ts">
  import { onMount } from 'svelte';
  export let posts = [];
  onMount(async () => {
    posts = await load();
  });
</script>

<div class="container">
  <section>
    <div class="intro">
      <h1>Matt Kilcup</h1>
      <p>Hi <span>👋</span> I'm Matt, a web developer from Phoenix, Az.</p>
      <p>I am passionate about my Faith, Family, green grass, web development, mechanical keyboards, and VS Code.</p>
    </div>
  </section>
  <section>
    <h2>Latest Posts</h2>
    <ul>
      {#each posts as { path, metadata: { title, tags } }}
        <li>
          <a href={`${path.replace('.md', '').replace('.svx', '')}`}>{title}</a>
          <p>{title}</p>
          <p>{path}</p>
        </li>
      {/each}
    </ul>
  </section>
</div>

<style>
  p {
    line-height: 150%;
    font-size: 1.25em;
  }
  .intro {
    padding: 2em 1em;
  }
  .greeting {
    font-family: 'Victor Mono', monospace;
  }

  span:hover {
    animation-name: howdy;
    animation-duration: 1s;
    animation-iteration-count: infinite;
    transform-origin: 60% 60%;
    display: inline-block;
  }

  @keyframes howdy {
    0% {
      transform: rotate(0deg);
    }
    10% {
      transform: rotate(14deg);
    }
    20% {
      transform: rotate(-8deg);
    }
    30% {
      transform: rotate(14deg);
    }
    40% {
      transform: rotate(-4deg);
    }
    50% {
      transform: rotate(10deg);
    }
    60% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(0deg);
    }
  }
</style>
