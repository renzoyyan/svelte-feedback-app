<script>
  import { fade, scale } from 'svelte/transition';
  import FeedbackItem from './FeedbackItem.svelte';

  // This is how to add props
  export let feedbacks = [];
</script>

{#each feedbacks as feedback (feedback.id)}
  <div in:scale out:fade={{ duration: 500 }}>
    <FeedbackItem item={feedback} on:delete-feedback />
  </div>
{/each}
