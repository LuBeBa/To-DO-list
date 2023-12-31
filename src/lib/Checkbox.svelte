<script lang="ts">
  import { fade } from "svelte/transition";
  import Checkmark from "./Checkmark.svelte";
  export let checked: boolean = false;
</script>

<button
  class="h-8 w-8 overflow-hidden rounded-md border border-gray-300"
  on:click={() => (checked = !checked)}
>
  {#if checked}
    <div
      transition:fade={{ duration: 100 }}
      class="flex h-full w-full items-center justify-center bg-blue-400 text-white"
    >
      <Checkmark />
    </div>
  {/if}
</button>
