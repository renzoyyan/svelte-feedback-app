<script>
  import Card from './ui/Card.svelte';
  import { FeedbackStore } from '../stores';

  export let item;

  /** We don't need the dispatch if we are using a store */
  // const dispatch = createEventDispatcher();

  const handleDelete = itemId => {
    // dispatch('delete-feedback', itemId);
    FeedbackStore.update(currentFeedback => {
      return currentFeedback.filter(item => item.id !== itemId);
    });
  };
</script>

<Card>
  <div class="num-display">
    {item.rating}
  </div>

  <button type="button" class="close" on:click={() => handleDelete(item.id)}>X</button>

  <p class="text-display">{item.text}</p>
</Card>

<style>
  .num-display {
    position: absolute;
    top: -10px;
    left: -10px;
    width: 50px;
    height: 50px;
    background-color: #ff6a95;
    color: #fff;
    border: 1px #eee solid;
    border-radius: 50%;
    padding: 10px;
    text-align: center;
    font-size: 19px;
  }

  .close {
    position: absolute;
    top: 10px;
    right: 20px;
    cursor: pointer;
    background: none;
    border: none;
  }
</style>
