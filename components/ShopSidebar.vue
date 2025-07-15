<template>
  <div class="sidebar">
    <form class="sidebar__form" @submit.prevent="submitSearch">
      <input v-model="item" placeholder="Search..." class="sidebar__input" type="text" />
      <button type="submit" class="sidebar__submit">
        <SearchIcon class="sidebar__icon" />
      </button>
    </form>

    <div class="sidebar__selects">
      <div class="sidebar__select">
        <select v-model="selectedCategory" class="sidebar__select-input" @change="emitCategory">
          <option value="">Category</option>
          <option v-for="category in categories" :key="category.value" :value="category.value">
            {{ category.label }}
          </option>
        </select>
        <button class="sidebar__select-mark">
          <MarkDown class="sidebar__select-icon" />
        </button>
      </div>

      <div class="sidebar__select">
        <select v-model="selectedSort" class="sidebar__select-input" @change="emitSort">
          <option value="">Sort By</option>
          <option
            v-for="sortOption in sortOptions"
            :key="sortOption.value"
            :value="sortOption.value"
          >
            {{ sortOption.label }}
          </option>
        </select>
        <button class="sidebar__select-mark">
          <MarkDown class="sidebar__select-icon" />
        </button>
      </div>
    </div>

    <InputSlider class="sidebar__slider" />

    <CheckboxSlider id="sale" v-model="isCheckedOnSale" class="sidebar__checkbox" label="On Sale" />

    <CheckboxSlider
      id="stock"
      v-model="isCheckedInStock"
      class="sidebar__checkbox"
      label="On Stock"
    />
  </div>
</template>

<script lang="ts" setup>
  import SearchIcon from 'SvgComponents/SearchIcon.vue'
  import MarkDown from 'SvgComponents/MarkDown.vue'

  const categories = [
    { value: "men's clothing", label: "men's clothing" },
    { value: 'jewelery', label: 'jewelery' },
    { value: 'electronics', label: 'electronics' },
    { value: "women's clothing", label: "women's clothing" },
  ]

  const sortOptions = [
    { value: 'price-desc', label: 'По убыванию стоимости' },
    { value: 'price-asc', label: 'По возрастанию стоимости' },
  ]

  const selectedCategory = ref('')
  const selectedSort = ref('')
  const isCheckedOnSale = ref(false)
  const isCheckedInStock = ref(false)
  const item = ref('')

  const emit = defineEmits<{
    (e: 'submitSearch', value: string): void
    (e: 'category', value: string): void
    (e: 'sort', value: string): void
  }>()

  const emitCategory = () => {
    emit('category', selectedCategory.value)
  }

  const emitSort = () => {
    emit('sort', selectedSort.value)
  }

  const submitSearch = () => {
    emit('submitSearch', item.value)
  }
</script>

<style lang="scss" scoped>
  .sidebar__select {
    position: relative;
    width: 100%;

    &-input {
      width: 100%;
      padding: 15px 12px;
      border: 1px solid var(--color-decorative);
      border-radius: 4px;
    }

    &-mark {
      position: absolute;
      right: 15px;
      bottom: 18px;
      pointer-events: none;
      background-color: transparent;
    }
  }

  .sidebar {
    display: flex;
    flex-direction: column;
    gap: 39px;

    &__checkbox {
      display: flex;
      flex-flow: row wrap;
      justify-content: space-between;
    }
  }

  .sidebar__selects {
    display: flex;
    flex-direction: column;
    gap: 16px;
    width: 100%;
  }

  .sidebar__form {
    position: relative;
    padding-bottom: 10px;
    border-bottom: 1px solid var(--color-decorative);
  }

  .sidebar__submit {
    position: absolute;
    right: 0;
    bottom: 5px;
    background-color: transparent;
  }

  .toggle-input {
    width: 0;
    height: 0;
    opacity: 0;
  }

  .slider {
    position: absolute;
    inset: 0;
    background-color: var(--color-text);
    border-radius: 34px;
    transition: background-color 0.3s;
  }

  .slider::before {
    position: absolute;
    bottom: 3.5px;
    left: 4px;
    width: 13px;
    height: 13px;
    content: '';
    background-color: white;
    border-radius: 50%;
    transition: transform 0.3s;
  }

  .toggle-input:checked + .slider {
    background-color: #4cd964;
  }

  .toggle-input:checked + .slider::before {
    transform: translateX(12px);
  }
</style>
