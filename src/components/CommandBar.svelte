<script>
  import { onMount, onDestroy } from 'svelte';

  let open  = $state(false);
  let query = $state('');

  const commands = [
    { key: 'email',    label: 'Copy email',    action: () => navigator.clipboard.writeText('montassare@dev.tn') },
    { key: 'linkedin', label: 'Open LinkedIn', action: () => window.open('https://linkedin.com/in/montassare', '_blank') },
    { key: 'github',   label: 'Open GitHub',   action: () => window.open('https://github.com/montassare', '_blank') },
    { key: 'pdf',      label: 'Download PDF',  action: () => window.print() },
    { key: 'close',    label: 'Close',         action: () => { open = false; } },
  ];

  let filtered = $derived(
    query
      ? commands.filter(c => c.label.toLowerCase().includes(query.toLowerCase()))
      : commands
  );

  function run(cmd) { cmd.action(); open = false; query = ''; }

  function onKey(e) {
    if ((e.metaKey || e.ctrlKey) && e.key === 'k') { e.preventDefault(); open = !open; query = ''; }
    if (e.key === 'Escape') { open = false; query = ''; }
  }

  onMount(() => window.addEventListener('keydown', onKey));
  onDestroy(() => window.removeEventListener('keydown', onKey));
</script>

<button
  class="no-print fixed bottom-5 right-5 z-50 flex items-center gap-2 rounded-full border px-3.5 py-2.5 font-mono transition-all duration-300 hover:scale-105 active:scale-95 sm:px-4 sm:py-3"
  style="font-size:0.7rem; border-color:var(--border-medium); background:var(--bg-secondary); color:var(--text-muted); box-shadow:0 8px 30px var(--glass-shadow);"
  onclick={() => { open = true; }}
  aria-label="Open command bar"
>
  <svg style="width:0.875rem;height:0.875rem;color:var(--text-secondary);" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
    <path stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16M4 18h16"/>
  </svg>
  <span class="hidden sm:inline">Menu</span>
</button>

{#if open}
<div class="fixed inset-0 z-50 flex items-start justify-center pt-[18vh]"
     style="background:rgba(0,0,0,0.55); backdrop-filter:blur(6px); -webkit-backdrop-filter:blur(6px);"
     role="dialog" aria-modal="true"
     onclick={(e) => { if (e.target === e.currentTarget) open = false; }}>
  <div class="w-full max-w-sm overflow-hidden rounded-2xl shadow-2xl mx-4"
       style="border:1px solid var(--border-medium); background:var(--bg-secondary);">
    <div class="flex items-center gap-3 px-4 py-3.5"
         style="border-bottom:1px solid var(--border-subtle);">
      <svg style="width:1rem;height:1rem;color:var(--text-muted);" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
          d="M21 21l-4.35-4.35M17 11A6 6 0 1 1 5 11a6 6 0 0 1 12 0z"/>
      </svg>
      <input autofocus bind:value={query} placeholder="Type a command…"
             style="flex:1; background:transparent; font-size:0.875rem; color:var(--text-primary); outline:none; font-family:inherit;" />
      <kbd
        style="font-size:0.65rem; color:var(--text-muted); background:var(--border-subtle); border-radius:4px; padding:2px 6px; font-family:monospace;"
      >esc</kbd>
    </div>
    <ul class="py-1.5">
      {#each filtered as cmd (cmd.key)}
        <li>
          <button class="flex w-full items-center gap-3 px-4 py-2.5 text-left text-sm transition-colors"
                  style="color:var(--text-secondary); background:transparent;"
                  onmouseover={(e) => e.currentTarget.style.background='var(--border-subtle)'}
                  onmouseleave={(e) => e.currentTarget.style.background='transparent'}
                  onfocus={(e) => e.currentTarget.style.background='var(--border-subtle)'}
                  onblur={(e) => e.currentTarget.style.background='transparent'}
                  onclick={() => run(cmd)}>
            {cmd.label}
          </button>
        </li>
      {/each}
      {#if filtered.length === 0}
        <li style="padding:0.75rem 1rem; font-size:0.75rem; color:var(--text-muted); font-family:monospace;">No results.</li>
      {/if}
    </ul>
  </div>
</div>
{/if}
