<script>
  let isDark = $state(true);

  function applyTheme(dark) {
    isDark = dark;
    const theme = dark ? 'dark' : 'light';
    document.documentElement.setAttribute('data-theme', theme);
    localStorage.setItem('theme', theme);
  }

  function toggle() {
    applyTheme(!isDark);
  }

  // Initialize from saved preference or system
  function init() {
    const saved = localStorage.getItem('theme');
    if (saved === 'light') {
      applyTheme(false);
    } else if (saved === 'dark') {
      applyTheme(true);
    } else {
      const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
      applyTheme(prefersDark);
    }
  }

  // Run immediately on mount
  import { onMount } from 'svelte';
  onMount(() => {
    init();
  });
</script>

<button
  onclick={toggle}
  aria-label={isDark ? 'Switch to light mode' : 'Switch to dark mode'}
  class="relative flex h-9 w-9 items-center justify-center rounded-full transition-all duration-300 hover:scale-110 active:scale-95"
  style="background: var(--border-subtle); color: var(--text-secondary);"
>
  <!-- Sun icon (visible in dark mode → switch to light) -->
  <svg
    class="absolute transition-all duration-400"
    style="width:1.125rem;height:1.125rem;opacity:{isDark ? 1 : 0};transform:rotate({isDark ? 0 : 90}deg);"
    fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="1.8"
    stroke-linecap="round" stroke-linejoin="round"
  >
    <circle cx="12" cy="12" r="5"/>
    <path d="M12 1v2M12 21v2M4.22 4.22l1.42 1.42M18.36 18.36l1.42 1.42M1 12h2M21 12h2M4.22 19.78l1.42-1.42M18.36 5.64l1.42-1.42"/>
  </svg>
  <!-- Moon icon (visible in light mode → switch to dark) -->
  <svg
    class="absolute transition-all duration-400"
    style="width:1rem;height:1rem;opacity:{isDark ? 0 : 1};transform:rotate({isDark ? -90 : 0}deg);"
    fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="1.8"
    stroke-linecap="round" stroke-linejoin="round"
  >
    <path d="M21 12.79A9 9 0 1111.21 3 7 7 0 0021 12.79z"/>
  </svg>
</button>
