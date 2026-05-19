<script>
  import ThemeToggle from './ThemeToggle.svelte';
</script>

<nav
  class="no-print fixed left-1/2 top-3 z-40 mx-auto w-[calc(100%-1.5rem)] max-w-xl -translate-x-1/2 rounded-full px-4 py-2.5 sm:top-4 sm:w-[calc(100%-2rem)] sm:px-5 sm:py-3 glass"
  aria-label="Main navigation"
>
  <div class="flex items-center justify-between">
    <!-- Brand -->
    <a
      href="#"
      class="text-sm font-semibold tracking-tight no-underline transition-colors duration-300 sm:text-base"
      style="color: var(--text-primary);"
      onclick={(e) => { e.preventDefault(); window.scrollTo({ top: 0, behavior: 'smooth' }); }}
    >
      MR
      <span class="ml-1.5 hidden text-xs font-light sm:inline" style="color: var(--text-muted);">
        Resume
      </span>
    </a>

    <!-- Right side -->
    <div class="flex items-center gap-1.5 sm:gap-2">
      <!-- CMD+K hint -->
      <span
        class="hidden rounded-full px-2.5 py-1 font-mono text-2xs font-medium sm:inline-block"
        style="background: var(--border-subtle); color: var(--text-muted);"
      >
        ⌘K
      </span>
      <ThemeToggle />
    </div>
  </div>
</nav>
