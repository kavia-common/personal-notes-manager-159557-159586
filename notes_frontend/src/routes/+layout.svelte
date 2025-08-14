<script lang="ts">
  import '../app.css';
  import TopBar from '$lib/components/TopBar.svelte';
  import Sidebar from '$lib/components/Sidebar.svelte';
  let { children } = $props();
</script>

<div class="layout">
  <TopBar />
  <div class="body">
    <Sidebar />
    <main class="content">
      {@render children()}
    </main>
  </div>
</div>

<style>
  .layout {
    display: grid;
    grid-template-rows: auto 1fr;
    min-height: 100vh;
    background: var(--color-surface-2);
  }
  .body {
    display: grid;
    grid-template-columns: auto 1fr;
    min-height: 0;
  }
  .content {
    min-height: 0;
    overflow: hidden;
    display: grid;
    grid-template-rows: 1fr;
    background: var(--color-background);
  }
</style>
