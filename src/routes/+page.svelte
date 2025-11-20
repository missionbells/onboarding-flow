<script>
  import { onMount } from 'svelte';
  import { goto } from '$app/navigation';

  onMount(() => {
    goto('/list-property');
  });
</script>

<div class="min-h-screen flex items-center justify-center bg-background">
  <p class="text-muted-foreground">Redirecting to onboarding...</p>
</div>
