<template>
  <div class="custom-select">
    <select ref="selectElement" v-model="selectedValue" class="custom-select__native" @click.stop>
      <option value="">Object</option>
      <option value="first">Первый элемент</option>
      <option value="second">Второй элемент</option>
      <option value="third">Третий элемент</option>
    </select>
    <button class="custom-select__button" type="button" aria-label="Toggle dropdown">
      <MarkDown class="custom-select__icon" />
    </button>
  </div>
</template>

<script setup lang="ts">
  import MarkDown from '../assets/pictures/svg/SvgComponents/MarkDown.vue'

  const selectedValue = defineModel()
</script>

<style scoped lang="scss">
  .custom-select {
    position: relative;
    display: inline-block;
    width: 100%;

    &__native {
      width: 100%;
      padding-bottom: 13px;
      font-size: var(--font-size-text-medium);
      font-weight: var(--font-weight-regular);
      line-height: var(--line-height-h4);
      color: var(--color-text);
      appearance: none;
      cursor: pointer;
      background-color: transparent;
      border-top: none;
      border-right: none;
      border-bottom: 1px solid var(--color-decorative);
      border-left: none;

      &:focus {
        outline: none;
        border-bottom-color: var(--color-accent);
      }
    }

    &__button {
      position: absolute;
      top: 50%;
      right: 5px;
      padding: 0;
      pointer-events: none;
      background: none;
      border: none;
      transform: translateY(-50%);
    }

    &__icon {
      width: 16px;
      height: 16px;
      color: var(--color-text);
    }
  }
</style>
