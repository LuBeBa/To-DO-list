<script lang="ts">
  export let value: string = "";
  export let placeholder: string = "";
</script>

<input
  type="text"
  class="h-10 w-full rounded-md border border-gray-300 px-4 ring-blue-500 transition-shadow focus:outline-none focus:ring-2"
  {placeholder}
  bind:value
/>
