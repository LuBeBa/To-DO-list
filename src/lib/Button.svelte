<script lang="ts">
  const variants = {
    primary: "bg-green-500 hover:bg-green-600 disabled:bg-green-500/70",
    secondary: "bg-gray-500 hover:bg-gray-600 disabled:bg-gray-500/70",
    danger: "bg-red-500 hover:bg-red-600 disabled:bg-red-500/70",
  } as const;

  type Variant = keyof typeof variants;
  export let variant: Variant = "primary";
  export let disabled = false;
</script>

<button
  class="h-10 rounded-md px-4 text-white transition-colors disabled:cursor-not-allowed disabled:bg-opacity-70 {variants[
    variant
  ]}"
  {disabled}
  on:click
>
  <slot />
</button>
