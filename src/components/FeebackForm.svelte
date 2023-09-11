<script>
  import { v4 as uuidv4 } from 'uuid';
  import { createEventDispatcher } from 'svelte';
  import RatingSelect from './RatingSelect.svelte';
  import Button from './ui/Button.svelte';
  import Card from './ui/Card.svelte';
  import { FeedbackStore } from '../stores';

  let text = '';
  let rating = 10;
  let btnDisabled = true;
  let min = 10;
  let errorMessage;

  const dispatch = createEventDispatcher();

  const handleInput = () => {
    if (text.trim().length <= min) {
      errorMessage = `Text must be at least ${min} characters`;
      btnDisabled = true;
    } else {
      errorMessage = null;
      btnDisabled = false;
    }
  };

  const handleRatingSelect = e => (rating = e.detail);

  const handleSubmit = () => {
    if (text.trim().length <= min) return;

    const newFeedback = {
      id: uuidv4(),
      text,
      rating: +rating,
    };

    FeedbackStore.update(currentFeedback => [newFeedback, ...currentFeedback]);
    text = '';
    btnDisabled = true;
  };
</script>

<Card>
  <h1 class="heading">How would you rate your service with us</h1>
  <form on:submit|preventDefault={handleSubmit}>
    <!-- Rating select -->
    <RatingSelect on:rating-select={handleRatingSelect} />
    <div class="form-group">
      <input
        type="text"
        bind:value={text}
        on:input={handleInput}
        placeholder="Tell us something that keeps you coming back"
      />
      <Button type="submit" label="Send" disabled={btnDisabled} />
    </div>

    {#if errorMessage}
      <p class="error-message">
        {errorMessage}
      </p>
    {/if}
  </form>
</Card>

<style>
  .heading {
    text-align: center;
    font-size: 1.8rem;
    max-width: 400px;
    margin: auto;
  }

  .form-group {
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 0.5rem 0.75rem;
    border: 1px #eee solid;
    border-radius: 0.5rem;
  }

  .form-group input {
    flex: 1 1 0%;
    border: 0;
    outline: none;
  }

  .error-message {
    font-size: 0.75rem;
    color: red;
    margin-top: 4px;
  }

  @media (max-width: 639px) {
    .heading {
      font-size: 1.5rem;
    }
  }
</style>
