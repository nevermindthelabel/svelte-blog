<script lang="ts">
  export let toggleTheme: svelte.JSX.MouseEventHandler<HTMLButtonElement>;
  export let currentTheme: string;
  import Icons from '../assets/svg/icons.svelte';
  import { isActive, url } from '@roxi/routify';
  const theRoutes = [
    { path: './index', name: 'home' },
    { path: './uses', name: 'uses' },
    { path: './blog', name: 'blog' }
  ];
</script>

<div class="wrapper">
  <div class={currentTheme}>
    <ul class="pages">
      {#each theRoutes as route}
        <li>
          <a class="{$isActive(route.path) ? 'active' : ''} {currentTheme}" href={$url(route.path)}>
            {route.name}
          </a>
        </li>
      {/each}
    </ul>
  </div>
  <button class="theme-toggle" on:click={toggleTheme}
    >{#if currentTheme === 'light'}
      <Icons theClass="dark-mode-btn" name="darkMode" width="20px" height="20px" fill="#000" />
    {:else}
      <Icons theClass="light-mode-btn" name="lightMode" width="20px" height="20px" fill="#fff" />
    {/if}
  </button>
</div>

<style>
  .dark.active,
  .light.active {
    font-weight: 900;
    font-style: italic;
    color: var(--svelte-orange);
  }
  ul {
    list-style-type: none;
    display: flex;
  }
  li {
    margin: 0.5em;
  }

  a {
    text-decoration: none;
    font-size: 20px;
    font-weight: bold;
    font-family: 'Victor Mono', monospace;
    transition: all 0.5s ease-out;
  }
  .wrapper {
    display: flex;
    padding: 15px;
  }
  .theme-toggle {
    text-decoration: none;
    margin-left: auto;
  }
  .theme-toggle:focus,
  .theme-toggle:hover {
    background-color: var(--svelte-orange);
  }
  .light {
    background: var(--light-mode-bg);
    color: var(--light-mode-text);
    transition: var(--transition);
  }
  .dark {
    background: var(--dark-mode-bg);
    color: var(--dark-mode-text);
    transition: var(--transition);
  }
  .light > ul > li > a {
    color: var(--light-mode-text);
  }
  .dark {
    color: var(--dark-mode-text);
  }
  .light {
    color: var(--svelte-orange);
  }
  a.dark:hover,
  a.dark:focus,
  a.light:hover,
  a.light:focus {
    color: var(--svelte-orange);
    font-style: italic;
    transition: all 0.5s ease-out;
  }
</style>
