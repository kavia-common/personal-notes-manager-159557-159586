<script lang="ts">
  import { onMount } from 'svelte';
  import { isAuthenticated } from '$lib/stores/auth';
  import { goto } from '$app/navigation';
  import NoteList from '$lib/components/NoteList.svelte';
  import NoteEditor from '$lib/components/NoteEditor.svelte';
  import { loadNotes } from '$lib/stores/notes';

  let error: string | null = null;

  onMount(async () => {
    if (!isAuthenticated()) {
      goto('/login');
      return;
    }
    try {
      await loadNotes();
    } catch (e: unknown) {
      error = e instanceof Error ? e.message : 'Failed to load notes';
    }
  });
</script>

<section class="notes-page">
  {#if error}
    <div class="error">{error}</div>
  {/if}
  <NoteList />
  <NoteEditor />
</section>

<style>
  .notes-page {
    display: grid;
    grid-template-columns: auto 1fr;
    min-height: 0;
    height: 100%;
  }
  .error {
    position: absolute;
    top: 64px;
    left: 50%;
    transform: translateX(-50%);
    background: #ffe9e9;
    color: #9f1d1d;
    border: 1px solid #ffcccc;
    padding: 0.5rem 0.75rem;
    border-radius: 8px;
  }
</style>
