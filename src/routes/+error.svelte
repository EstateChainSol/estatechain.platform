<script>
  import { onMount } from 'svelte';
  import { goto } from '$app/navigation';
  import { base } from '$app/paths';

  onMount(() => {
    // Get the path from the URL
    const path = window.location.pathname;
    // Remove the base path if it exists
    const cleanPath = path.replace(base, '');
    // Redirect to the correct route
    goto(cleanPath);
  });
</script>

<div class="min-h-screen flex items-center justify-center">
  <div class="text-center">
    <h1 class="text-4xl font-bold mb-4">Redirecting...</h1>
    <p class="text-gray-400">Please wait while we redirect you to the correct page.</p>
  </div>
</div> 