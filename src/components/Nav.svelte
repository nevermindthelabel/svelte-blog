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
  <div class="header {currentTheme}">
    <ul class="pages">
      {#each theRoutes as route}
        <li>
          <a
            aria-current={$isActive(route.path) ? 'page' : false}
            class="{$isActive(route.path) ? 'active' : ''} {currentTheme}"
            href={$url(route.path)}
          >
            {route.name}
          </a>
        </li>
      {/each}
    </ul>
  </div>
  <button
    type="button"
    class="theme-toggle"
    aria-pressed="false"
    title="switch {currentTheme === 'light' ? 'to dark' : 'to light'} mode"
    on:click={toggleTheme}
  >
    {#if currentTheme === 'light'}
      <Icons theClass="dark-mode-btn" name="darkMode" width="30px" height="30px" fill={'#000'} />
    {:else}
      <Icons theClass="light-mode-btn" name="lightMode" width="30px" height="30px" fill={'#fff'} />
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
    padding: 30px 40px;
  }

  .theme-toggle {
    text-decoration: none;
    margin-left: auto;
  }

  .theme-toggle:focus {
    outline: 2px solid green;
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

  a.dark:hover,
  a.dark:focus,
  a.light:hover,
  a.light:focus {
    color: var(--svelte-orange);
    font-style: italic;
    transition: all 0.5s ease-out;
  }

  @media (max-width: 35em) {
    .header {
      display: block;
    }

    .wrapper,
    ul {
      flex-direction: column;
      align-items: flex-start;
    }

    .wrapper {
      padding: min(30vh, 5rem) 2em;
    }

    .dark .wrapper {
      background: var(--dark-mode-bg);
    }

    .light .wrapper {
      background: var(--light-mode-bg);
    }

    .theme-toggle {
      margin: 0.5em;
    }
  }
</style>
