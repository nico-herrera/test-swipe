<script lang="ts">
  import { CardSwiper } from "$lib/CardSwiper";
  import { fade } from "svelte/transition";

  let swipe: (direction?: "left" | "right") => void;

  let passedOnCoins = [];

  let people = [
    {
      name: "Lucas",
      age: 40,
      description: "Loves to dance in the rain.",
    },
    {
      name: "Benjamin",
      age: 28,
      description: "Eats pizza with a fork.",
    },
    {
      name: "Noah",
      age: 49,
      description: "Talks to plants.",
    },
    {
      name: "Emily",
      age: 45,
      description: "Sleeps with socks on.",
    },
    {
      name: "Ava",
      age: 43,
      description: "Thinks they can speak to animals.",
    },
    {
      name: "Sophia",
      age: 23,
      description: "Obsessed with organizing.",
    },
    {
      name: "Charlotte",
      age: 41,
      description: "Afraid of shadows.",
    },
    {
      name: "Olivia",
      age: 23,
      description: "Collects rare pebbles.",
    },
    {
      name: "Isabella",
      age: 42,
      description: "Always forgets why they walked into a room.",
    },
    {
      name: "Jacob",
      age: 24,
      description: "Can recite movies backwards.",
    },
  ];

  let thresholdPassed = 0;
</script>

<div
  class="h-[100svh] w-[100svw] p-2 flex-col items-center justify-center overflow-hidden"
>
  <div class="w-1/2 h-3/4 mx-auto">
    <div class="w-full h-full max-w-xl relative">
      <CardSwiper
        bind:swipe
        cardData={(index) => {
          let i = Math.floor(Math.random() * people.length);
          let j = Math.floor(Math.random() * people.length);
          return {
            title: people[i].name + ", " + people[i].age,
            description: people[j].description,
            image: `/profiles/${index % 14}.png`,
            marketData: {
              marketCap: "5m",
              fdv: "1m",
              supply: "1b",
            },
          };
        }}
        on:swiped={(e) => {
          console.log(e.detail);
          if (e.detail.direction === "left") {
            passedOnCoins.push(e.detail.data);
          }
          console.log("Passed on profiles:", passedOnCoins);
        }}
        bind:thresholdPassed
      />
    </div>
    <div class="flex items-center justify-center mt-4 gap-8">
      <button
        class="h-12 w-12 flex items-center justify-center text-red-500 bg-red-500/50 backdrop-blur-sm rounded-full z-10 text-3xl"
        on:click={() => swipe("left")}
      >
        x
      </button>
      <button
        class="h-12 w-12 flex items-center justify-center text-white bg-gray-800 backdrop-blur-sm rounded-full z-10 text-lg"
      >
        icon
      </button>
      <button
        class="h-12 w-1/2 bg-green-500/50 backdrop-blur-sm rounded-full z-10 text-3xl flex justify-between items-center px-4"
        on:click={() => swipe("right")}
      >
        <p>x</p>
        <p>Buy $5</p>
      </button>
    </div>
  </div>
  {#if thresholdPassed > 0}
    <div
      transition:fade={{ duration: 200 }}
      class="absolute w-full h-full inset-0 bg-black/20 backdrop-blur-sm flex items-center justify-center text-5xl pointer-events-none text-green-500"
    >
      $5 of Satard purchased
    </div>
  {/if}
</div>
