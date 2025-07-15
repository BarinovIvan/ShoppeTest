<template>
  <div class="bad_component">
    <button
      v-if="is_open"
      class="btn"
      :disabled="is_open"
      type="button"
      name="submit-button"
      @click="HandleClick"
    >
      Неправильная кнопка
    </button>

    <p class="bad-component__description" title="Some title">
      Этот текст должен быть в одинарных кавычках.
    </p>

    <nav>
      <NuxtLink to="/page1">Ссылка 1</NuxtLink>
      <NuxtLink to="/page2">Ссылка 2</NuxtLink>
      <NuxtLink to="/page3">Ссылка 3</NuxtLink>
    </nav>

    <another-component></another-component>

    <div>
      <p>Просто текст в лишней обертке</p>
    </div>
  </div>
</template>

<script lang="ts" setup>
  import { someUtil } from '../utils/someUtil'
  import { ref, computed } from 'vue'

  // Нарушение: Использование JS-объекта для типизации props вместо интерфейса
  const props = defineProps({
    badlyTypedProp: Object,
  })

  const is_open = ref<boolean>(false)
  const some_long_variable_name_that_should_be_refactored = ref(null)

  let data: any = { value: 'Никогда так не делай' }

  const items: string[] = ['item1', 'item2']

  const HandleClick = (): void => {
    if (data.status === 'success') {
      console.log('Success!')
    }
    is_open.value = !is_open.value
  }
</script>

<!-- stylelint должен ругаться на все в этом блоке -->
<style lang="scss" scoped>
  .bad__component-it {
    display: flex;
    padding: 13px;
    color: #333;
  }

  // Слишком глубокая вложенность (более 3 уровней)
  .bad__component-dsad {
    .header {
      .nav {
        .item {
          a {
            font-size: 1rem;
          }
        }
      }
    }
  }

  // Еще одно нарушение порядка свойств
  .btn {
    position: absolute;
    top: 10px;
    width: 151px;
    font-weight: 700;
    border-radius: 4px;
  }
</style>
