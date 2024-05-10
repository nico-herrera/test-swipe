<script lang="ts">
  export let element: HTMLElement;

  export let color: string = "";
  export let title: string = "";
  export let description: string = "";
  export let image: string | undefined = undefined;
  export let marketData: any = {};
</script>

<div
  class="w-full h-full absolute cursor-grab ease-in-out rounded-xl touch-none select-none border border-black bg-white {color}"
  bind:this={element}
>
  {#key image}
    {#if image}
      <img
        class="w-full h-full rounded-xl object-cover"
        src={image}
        alt={title}
      />
    {/if}
  {/key}
  <div
    class="absolute inset-0 bg-gradient-to-t from-white/80 via-white/0 rounded-b-xl"
  ></div>
  <div class="p-4 absolute bottom-0 w-full flex justify-center">
    <div class="flex items-center flex-col">
      <h3 class="text-3xl font-semibold pb-4">{title}</h3>
      <p>{description}</p>
      <p>Market Cap: {marketData.marketCap}</p>
      <p>FDV: {marketData.fdv}</p>
      <p>Supply: {marketData.supply}</p>
    </div>
  </div>
</div>
