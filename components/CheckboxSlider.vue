<template>
  <label class="checkbox-slider">
    {{ props.label }}
    <div class="toggle-switch">
      <input :id="props.id" v-model="model" type="checkbox" class="toggle-input" />
      <span class="slider"></span>
    </div>
  </label>
</template>

<script lang="ts" setup>
  import { defineModel } from 'vue'

  const model = defineModel<boolean>()

  interface Props {
    label: string
    id: string
  }

  const props = defineProps<Props>()
</script>

<style lang="scss" scoped>
  .checkbox-slider {
    display: flex;
    gap: 10px;
    align-items: center;
    justify-content: space-between;
    cursor: pointer;
  }

  .toggle-switch {
    position: relative;
    display: inline-block;
    width: 33px;
    height: 20px;
  }

  .toggle-input {
    position: absolute;
    width: 0;
    height: 0;
    opacity: 0;

    &:checked + .slider {
      background-color: #4cd964;

      &::before {
        transform: translateX(13px);
      }
    }

    &:focus-visible + .slider {
      box-shadow: 0 0 0 2px rgb(0 0 0 / 10%);
    }
  }

  .slider {
    position: absolute;
    inset: 0;
    cursor: pointer;
    background-color: var(--color-text);
    border-radius: 34px;
    transition: 0.3s;

    &::before {
      position: absolute;
      bottom: 3.5px;
      left: 4px;
      width: 13px;
      height: 13px;
      content: '';
      background-color: white;
      border-radius: 50%;
      transition: 0.3s;
    }
  }
</style>
