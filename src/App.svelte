<script>
  import FeebackForm from './components/FeebackForm.svelte';
  import FeedbackList from './components/FeedbackList.svelte';
  import FeedbackStats from './components/FeedbackStats.svelte';

  let feedbacks = [
    {
      id: 1,
      rating: 10,
      text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.',
    },
    {
      id: 2,
      rating: 9,
      text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.',
    },
    {
      id: 3,
      rating: 8,
      text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.',
    },
  ];

  // $ -> is reactivity, it is more likely a useState
  $: count = feedbacks.length;
  $: average = feedbacks.reduce((total, curr) => total + curr.rating, 0) / count;

  const handleAddFeedback = e => {
    const newFeedback = e.detail;
    feedbacks = [newFeedback, ...feedbacks];
  };
  const handleDeleteFeedback = e => {
    const itemId = e.detail;

    feedbacks = feedbacks.filter(fb => fb.id !== itemId);
  };
</script>

<main class="container">
  <FeebackForm on:add-feedback={handleAddFeedback} />
  <FeedbackStats {count} {average} />
  <FeedbackList {feedbacks} on:delete-feedback={handleDeleteFeedback} />
</main>

<style>
</style>
