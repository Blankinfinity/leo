<svelte:options tag="leo-label" />

<script context="module" lang="ts">
  export const colors = [
    'gray',
    'secondary',
    'primary',
    'red',
    'yellow',
    'green',
    'blue',
    'purple',
    'pink',
    'teal',
    'CTA'
  ] as const
  export type Color = (typeof colors)[number]

  export const modes = ['default', 'loud'] as const
  export type Mode = (typeof modes)[number]
</script>

<script lang="ts">
  export let mode: Mode = 'default'
  export let color: Color = 'gray'

  $: background =
    color === 'CTA'
      ? `var(--gradient-hero)`
      : mode === 'loud'
      ? `var(--color-${color}-40)`
      : `var(--color-${color}-10)`
  $: text =
    color === 'CTA'
      ? `var(--color-white)`
      : mode === 'loud'
      ? `var(--color-${color}-10)`
      : `var(--color-${color}-50)`
</script>

<div class="leo-label" style:background style:color={text}>
  <div class="content">
    <slot>Label</slot>
  </div>
</div>

<style lang="scss">
  .leo-label {
    --icon-size: var(--leo-label-icon-size, 13px);
    --font-text: var(--leo-label-font-text, var(--font-components-label));
    --padding: var(--leo-label-padding, var(--spacing-4));
    --radius: var(--leo-label-radius, var(--radius-4));

    --leo-icon-size: var(--icon-size);

    display: inline-block;
    border-radius: var(--radius);
    padding: var(--padding);
    font: var(--font-text);
  }

  .content {
    display: flex;
    flex-direction: row;
    gap: 4px;
    justify-content: space-between;
    align-items: center;
  }
</style>
