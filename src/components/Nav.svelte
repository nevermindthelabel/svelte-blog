<script>
  export let toggleTheme;
  export let currentTheme;
  import Icons from '../assets/svg/icons.svelte';
  $: console.log(currentTheme);
</script>

<div class="wrapper">
  <div class={currentTheme}>routes go here</div>
  <button class="theme-toggle" on:click={toggleTheme}
    >{#if currentTheme === 'light'}
      <Icons theClass="dark-mode-btn" name="darkMode" width="20px" height="20px" fill="#000" />
    {:else}
      <Icons theClass="light-mode-btn" name="lightMode" width="20px" height="20px" fill="#fff" />
    {/if}
  </button>
</div>

<style>
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
    background-color: orange;
  }
  .light {
    background: #fff;
    color: #2b2e31;
    transition: var(--transition);
  }
  .dark {
    background: #2b2e31;
    color: #fff;
    transition: var(--transition);
  }
</style>
