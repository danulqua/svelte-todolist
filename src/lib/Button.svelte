<script>
  export let size = 'small';
  export let shadow = false;
  export let bgColor = undefined;
  export let color = undefined;

  let isLeftHovered = false;
</script>

<!-- One of the use cases when it's ok to use $$restProps -->
<button
  on:click
  style:color
  style:background-color={bgColor}
  class:size-sm={size === 'small'}
  class:size-lg={size === 'large'}
  class:shadow
  {...$$restProps}
>
  {#if $$slots.left}
    <div
      class="left-content"
      on:mouseenter={() => (isLeftHovered = true)}
      on:mouseleave={() => (isLeftHovered = false)}
    >
      <slot name="left" />
    </div>
  {/if}
  <slot {isLeftHovered}>Fallback</slot>
</button>

<style lang="scss">
  button {
    display: flex;
    align-items: center;
    gap: 10px;
    border: none;
    outline: none;
    background-color: $color-main;
    border-radius: 10px;
    font-size: 18px;
    cursor: pointer;

    &.size-sm {
      padding: 15px 20px;
    }

    &.size-lg {
      padding: 20px 25px;
      font-size: 22px;
    }

    &.shadow {
      box-shadow: 0 0 10px $color-main;
    }

    &:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }

    &:hover {
      background-image: linear-gradient(rgba(0, 0, 0, 0.2) 0 0);
    }

    &:active {
      background-image: linear-gradient(rgba(255, 255, 255, 0.2) 0 0);
    }
  }
</style>
