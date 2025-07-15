<template>
  <button :class="buttonClasses">
    <slot></slot>
  </button>
</template>

<script setup lang="ts">
  import { computed } from 'vue'
  type ButtonVariant = 'primary' | 'secondary' | 'special'
  type ButtonSize = 'xl' | 'l' | 'm'

  interface Props {
    variant: ButtonVariant
    size: ButtonSize
  }

  const props = defineProps<Props>()

  const buttonClasses = computed(() => ({
    primary: props.variant === 'primary',
    secondary: props.variant === 'secondary',
    special: props.variant === 'special',
    'button__size-xl': props.size === 'xl',
    'button__size-l': props.size === 'l',
    'button__size-m': props.size === 'm',
  }))
</script>

<style lang="scss" scoped>
  @mixin base-button {
    width: 100%;
    padding: 12px;
    font-family: 'DM Sans';
    font-size: 16px;
    font-weight: var(--font-weight-bold);
    border: 2px solid var(--color-main);
    border-radius: 4px;
    transition:
      background-color 0.4s ease,
      color 0.4s ease;
  }

  @mixin primary-colors {
    color: var(--color-contrast);
    background-color: var(--color-main);
  }

  @mixin secondary-colors {
    color: var(--color-main);
    background-color: var(--color-contrast);
  }

  .primary {
    @include base-button;
    @include primary-colors;

    &:hover {
      @include secondary-colors;

      border: 2px solid var(--color-main);
    }
  }

  .secondary {
    @include base-button;
    @include secondary-colors;

    &:hover {
      @include primary-colors;
    }
  }

  .special {
    @include base-button;

    font-size: clamp(0.75rem, 0.574rem + 0.751vw, 1.25rem);
    color: var(--color-contrast);
    background-color: var(--color-transparent);
    border: 2px solid var(--color-contrast);
    border-radius: 6px;

    &:hover {
      @include secondary-colors;
    }
  }

  .button__size-xl {
    max-width: 500px;
  }

  .button__size-l {
    max-width: 197px;
  }

  .button__size-m {
    max-width: 123px;
  }

  @media (width <= 375px) {
    @mixin base-button {
      padding: 6px 9px;
      font-size: 12px;
      line-height: 20px;
      border-radius: 4px;
    }

    .special {
      max-width: 102px;
      max-height: 32px;
      padding: 6px 9px;
    }

    .primary,
    .secondary,
    .special {
      @include base-button;
    }

    .button__size-xl {
      max-width: 100%;
    }

    .button__size-l {
      max-width: 100%;
    }

    .button__size-m {
      max-width: 100%;
    }
  }
</style>
