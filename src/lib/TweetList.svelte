<script>
  import Tweet from "$lib/Tweet.svelte";
  import { fly, slide } from "svelte/transition";
  import { cubicOut } from "svelte/easing";

  export let tweets;
  export let extendedTweets;
  export let foundIn = [];

  let extended = false;
</script>

<div class="p-5 border-2 border-orange-200 bg-white xl:min-w-0 xl:basis-1/2">
  <span
    class="block text-center text-lg text-orange-500 font-bold tracking-tighter"
    >LATEST EVENTS</span
  >

  <div class="flex flex-col">
    {#each tweets as tweet, tweetIndex}
      <Tweet
        time={tweet.created_at}
        message={tweet.content}
        pubkey={tweet.pubkey}
        foundIn={foundIn[tweetIndex]}
      />
    {/each}
  </div>
  {#if extended}
    <div
      class="flex flex-col"
      transition:fly={{ y: -10, duration: 200, easing: cubicOut }}
    >
      {#each extendedTweets as tweet, tweetIndex}
        <Tweet
          time={tweet.created_at}
          message={tweet.content}
          pubkey={tweet.pubkey}
          foundIn={foundIn[tweetIndex]}
        />
      {/each}
    </div>
  {/if}

  {#if !extended}
    <!-- button -->
    <div class="flex mt-5" in:fly={{ y: 10, duration: 200, easing: cubicOut }}>
      <div class="flex-1" />
      <div
        class="flex items-center space-x-1 hover:cursor-pointer"
        on:click={() => {
          extended = !extended;
        }}
      >
        <span class="text-stone-500 font-mono tracking-widest">more</span>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-4 w-4 text-stone-400"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          stroke-width="2"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M19 9l-7 7-7-7"
          />
        </svg>
      </div>
    </div>
  {/if}
</div>
