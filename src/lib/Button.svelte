<script lang="ts">
  const variants = {
    primary: "bg-blue-500 hover:bg-blue-600 disabled:bg-blue-400",
    secondary: "bg-gray-500 hover:bg-gray-600 disabled:bg-gray-400",
    danger: "bg-red-500 hover:bg-red-600 disabled:bg-red-400",
  } as const;

  type Variant = keyof typeof variants;
  export let variant: Variant = "primary";
  export let disabled = false;
</script>

<button
  class="h-10 rounded-md px-4 text-white transition-colors disabled:cursor-not-allowed {variants[
    variant
  ]}"
  {disabled}
  on:click
>
  <slot />
</button>
