<script lang="ts">
  import { onMount } from "svelte";
  import Button from "./lib/Button.svelte";
  import TextInput from "./lib/TextInput.svelte";
  import type { Task as ITask } from "./types";
  import Task from "./lib/Task.svelte";

  let loaded = false;

  let maxID = 0;
  let taskInput = "";
  let tasks: ITask[] = [];

  // This prevents from a race condition where the tasks are reset before they are loaded from localStorage
  $: loaded && localStorage.setItem("tasks", JSON.stringify(tasks));

  $: maxID = Math.max(...tasks.map((t) => t.id), 0);

  onMount(() => {
    tasks = JSON.parse(localStorage.getItem("tasks") || "[]");
    loaded = true;
  });
</script>

<div class="flex h-full items-center justify-center p-4">
  <div
    class="flex w-full max-w-md flex-col overflow-hidden rounded-lg bg-white shadow-md"
  >
    <h1
      class="w-full border-b border-gray-200 bg-gray-50 py-2 text-center text-3xl font-bold text-blue-500"
    >
      To-Do Liste
    </h1>
    <div class="flex flex-col gap-2 p-2">
      {#each tasks as task (task.id)}
        <Task
          bind:task
          on:remove={() => {
            tasks = tasks.filter((t) => t !== task);
          }}
        />
      {/each}
      {#if tasks.length === 0}
        <p class="flex h-12 items-center justify-center text-gray-500">
          Keine Aufgaben vorhanden
        </p>
      {/if}
      <div class="flex flex-col gap-2 rounded-md bg-gray-50 p-2">
        <div class="flex flex-row gap-2">
          <TextInput placeholder="Neue Aufgabe" bind:value={taskInput} />
          <Button
            variant="primary"
            disabled={taskInput.length === 0}
            on:click={() => {
              tasks = [
                ...tasks,
                {
                  id: ++maxID,
                  text: taskInput,
                  done: false,
                },
              ];
              taskInput = "";
            }}
          >
            Hinzufügen
          </Button>
        </div>
        <Button
          variant="danger"
          on:click={() => {
            tasks = tasks.filter((t) => !t.done);
          }}
        >
          Alle erledigten Aufgaben entfernen
        </Button>
      </div>
    </div>
  </div>
</div>
