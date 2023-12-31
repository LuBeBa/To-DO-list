<script lang="ts">
  import Checkbox from "./Checkbox.svelte";
  import type { Task } from "../types";
  import { createEventDispatcher } from "svelte";
  export let task: Task;

  const eventDispatcher = createEventDispatcher<{
    remove: null;
  }>();
</script>

<div
  class="flex items-center gap-2 rounded-md bg-gray-100 p-2 transition-colors"
>
  <Checkbox bind:checked={task.done} />
  <span class="mr-auto text-lg">{task.text}</span>
  <button
    class="h-8 w-8 rounded-md bg-red-500 text-lg font-bold text-white transition-colors hover:bg-red-600 disabled:bg-red-400"
    on:click={() => {
      eventDispatcher("remove");
    }}
    >X
  </button>
</div>
