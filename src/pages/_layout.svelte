<script lang="ts">
  import { onMount } from 'svelte';
  import Nav from '../components/Nav.svelte';
  import Footer from '../components/Footer.svelte';
  import Icons from '../assets/svg/icons.svelte';
  const STORAGE_KEY = 'theme';
  const DARK_PREFERENCE = '(prefers-color-scheme: dark)';
  const LIGHT_PREFERENCE = '(prefers-color-scheme: light)';
  let currentTheme;
  let isExpanded = false;

  const THEMES = {
    DARK: 'dark',
    LIGHT: 'light'
  };

  const applyTheme = () => {
    const preferredTheme = prefersDarkThemes() ? THEMES.DARK : prefersLightThemes() ? THEMES.LIGHT : null;
    currentTheme = localStorage.getItem(STORAGE_KEY) ?? preferredTheme;
  };

  const prefersDarkThemes = () => window.matchMedia(DARK_PREFERENCE).matches;
  const prefersLightThemes = () => window.matchMedia(LIGHT_PREFERENCE).matches;

  const toggleTheme = () => {
    if (prefersDarkThemes() && currentTheme === THEMES.LIGHT) {
      window.document.body.classList.remove('light');
      window.document.body.classList.add('dark');
      localStorage.removeItem(STORAGE_KEY);
    } else if (prefersDarkThemes() && currentTheme === THEMES.DARK) {
      localStorage.removeItem(STORAGE_KEY);
      localStorage.setItem(STORAGE_KEY, THEMES.LIGHT);
      window.document.body.classList.remove('dark');
      window.document.body.classList.add('light');
    } else if (prefersLightThemes() && currentTheme === THEMES.DARK) {
      localStorage.removeItem(STORAGE_KEY);
      window.document.body.classList.remove('dark');
      window.document.body.classList.add('light');
      currentTheme = THEMES.LIGHT;
    } else if (prefersLightThemes() && !currentTheme) {
      localStorage.removeItem(STORAGE_KEY);
      localStorage.setItem(STORAGE_KEY, THEMES.DARK);
      window.document.body.classList.toggle('dark');
      window.document.body.classList.toggle('light');
      currentTheme = THEMES.DARK;
    } else if (prefersLightThemes() && currentTheme === THEMES.LIGHT) {
      localStorage.removeItem(STORAGE_KEY);
      localStorage.setItem(STORAGE_KEY, THEMES.DARK);
      window.document.body.classList.toggle('dark');
      window.document.body.classList.toggle('light');
      currentTheme = THEMES.DARK;
    } else if (prefersLightThemes() && currentTheme === THEMES.DARK) {
      localStorage.removeItem(STORAGE_KEY);
      currentTheme = THEMES.LIGHT;
      window.document.body.classList.toggle('dark');
      window.document.body.classList.toggle('light');
    }
    applyTheme();
  };

  onMount(() => {
    applyTheme();
    window.matchMedia(DARK_PREFERENCE).addEventListener('change', applyTheme);
    window.matchMedia(LIGHT_PREFERENCE).addEventListener('change', applyTheme);
  });
</script>

<body class={currentTheme}>
  <header class={currentTheme}>
    <div class="toggle">
      <button class="mobile" on:click={() => (isExpanded = !isExpanded)}>
        {#if isExpanded}
          <Icons theClass="fries" name="fries" width="20px" height="20px" fill={'currentColor'} />
        {:else}
          <Icons theClass="burger" name="hamburger" width="20px" height="20px" fill={'#fff'} />
        {/if}
      </button>
    </div>
    <Nav {toggleTheme} {currentTheme} {isExpanded} />
  </header>

  <main class={currentTheme}>
    <slot />
  </main>
  <footer>
    <Footer />
  </footer>
</body>

<style>
  @import 'victormono';
  :global(p) {
    font-family: 'Victor Mono', monospace;
  }
  :global(header),
  :global(main) {
    position: relative;
    z-index: 1;
  }
  :global(main) {
    display: flex;
    background: white;
    justify-content: center;
    min-height: 100vh;
    padding: 0 1em;
  }
  :global(body) {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    width: 100%;
  }
  :global(Footer) {
    position: sticky;
    bottom: 0;
    background: #2b2e31;
    display: grid;
    place-items: center center;
    text-align: center;
    color: #fff;
    font-family: monospace;
  }
  .toggle {
    display: none;
  }
  @media (max-width: 35em) {
    header.dark,
    header.light {
      z-index: 2;
      position: fixed;
      inset: 0 0 0 10%;
      /* display: none; */
    }
    .toggle {
      display: block;
      position: absolute;
      top: 1rem;
      right: 1rem;
      z-index: 10;
    }
  }
</style>
