<template>
  <div class="text-input">
    <input
      v-model="model"
      class="input"
      :type="type"
      :class="inputSize"
      :placeholder="placeholder"
      @blur="handleBlur"
    />
    <p v-if="props.error" class="error-message">
      {{ props.error }}
    </p>
  </div>
</template>

<script lang="ts" setup>
  type size = 'small' | 'medium'
  type error = string | ''

  interface Props {
    size: size
    error?: error
    placeholder: string
    type?: string
  }

  const props = withDefaults(defineProps<Props>(), {
    type: 'text',
  })

  const model = defineModel<string>()
  const emit = defineEmits(['blur']) // Добавлено здесь

  const inputSize = computed(() => ({
    'input-small': props.size === 'small',
    'input-medium': props.size === 'medium',
  }))

  const handleBlur = () => {
    emit('blur')
  }
</script>

<style lang="scss" scoped>
  .text-input {
    position: relative;
  }

  .input {
    padding-bottom: 13px;
    border-bottom: 1px solid var(--color-decorative);

    &-small {
      width: 100%;
      min-width: 200px;
      max-width: 396px;
      padding-right: 30px;
    }

    &-medium {
      width: 100%;
      font-size: var(--font-size-text-medium);
      font-weight: var(--font-weight-regular);
      line-height: var(--line-height-h4);
    }
  }

  @media (width < 376px) {
    .input {
      padding-bottom: 6px;
      font-size: 12px;

      &-small {
        width: 100%;
        min-width: 200px;
        max-width: 396px;
        padding-right: 30px;
      }

      &-medium {
        width: 100%;
        font-size: var(--font-size-text-medium);
        font-weight: var(--font-weight-regular);
        line-height: var(--line-height-h4);
      }
    }
  }
</style>
