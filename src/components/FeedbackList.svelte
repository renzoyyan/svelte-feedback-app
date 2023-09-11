<script>
  import { fade, scale } from 'svelte/transition';
  import FeedbackItem from './FeedbackItem.svelte';
  import { FeedbackStore } from '../stores';
  import { onDestroy, onMount } from 'svelte';

  // This is how to add props
  // export let feedbacks = [];

  let feedbacks = [];

  /** longer way to access store */

  // const unsubscribe = FeedbackStore.subscribe(data => (feedbacks = data));

  /**  u can fetch data here */
  // onMount(() => {
  //   console.log('mounted');
  // });

  /**  this is similar to return in useEffect */
  // onDestroy(() => {
  //   unsubscribe();
  // });
</script>

<!-- $FeedbackStore is a shorter way to access the store and it will also unsubscribe automatically just like the above -->

{#each $FeedbackStore as feedback (feedback.id)}
  <div in:scale out:fade={{ duration: 500 }}>
    <FeedbackItem item={feedback} />
  </div>
{/each}
