<script lang="ts">
  import AuthForm from '$lib/components/AuthForm.svelte';
  import { login, isAuthenticated } from '$lib/stores/auth';
  import { goto } from '$app/navigation';
  import { onMount } from 'svelte';

  onMount(() => {
    if (isAuthenticated()) goto('/notes');
  });

  async function handleLogin(email: string, password: string) {
    await login(email, password);
    goto('/notes');
  }
</script>

<div class="center">
  <AuthForm mode="login" onSubmit={handleLogin} />
  <div class="swap">
    Don't have an account?
    <a href="/register">Create one</a>
  </div>
</div>

<style>
  .center {
    display: grid;
    place-items: center;
    padding: 2rem 1rem;
  }
  .swap {
    margin-top: 0.75rem;
    color: var(--color-text-secondary);
    text-align: center;
  }
  a {
    color: var(--color-primary);
    text-decoration: none;
    font-weight: 600;
    margin-left: 0.25rem;
  }
</style>
