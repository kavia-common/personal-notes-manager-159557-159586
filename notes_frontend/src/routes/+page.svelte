<script lang="ts">
  import { onMount } from 'svelte';
  import { isAuthenticated } from '$lib/stores/auth';
  import { goto } from '$app/navigation';

  onMount(() => {
    if (isAuthenticated()) {
      goto('/notes');
    } else {
      goto('/login');
    }
  });
</script>
