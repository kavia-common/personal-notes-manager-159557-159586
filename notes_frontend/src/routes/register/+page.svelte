<script lang="ts">
  import AuthForm from '$lib/components/AuthForm.svelte';
  import { register, isAuthenticated } from '$lib/stores/auth';
  import { goto } from '$app/navigation';
  import { onMount } from 'svelte';

  onMount(() => {
    if (isAuthenticated()) goto('/notes');
  });

  async function handleRegister(email: string, password: string) {
    await register(email, password);
    goto('/notes');
  }
</script>

<div class="center">
  <AuthForm mode="register" onSubmit={handleRegister} />
  <div class="swap">
    Already have an account?
    <a href="/login">Log in</a>
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
