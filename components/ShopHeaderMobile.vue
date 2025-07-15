<template>
  <div>
    <div class="shop-header">
      <h3 class="shop-header__heading">Shop</h3>
      <button class="shop-header__button" @click="toggleDropFilters">
        <SettingsGoldIcon />
        <span class="shop-header__button-heading">Filters</span>
      </button>
    </div>

    <transition name="slide">
      <div v-if="filtersIsOpen === true" class="filters">
        <div class="filters__header">
          <h1 class="filters__header-heading">Filters</h1>
          <button>
            <XIcon @click="toggleDropFilters" />
          </button>
        </div>

        <ShopSidebar />
      </div>
    </transition>
  </div>
</template>

<script setup lang="ts">
  import SettingsGoldIcon from '../assets/pictures/svg/SvgComponents/SettingsGoldIcon.vue'
  import XIcon from '../assets/pictures/svg/SvgComponents/XIcon.vue'

  const filtersIsOpen = ref<boolean>(false)

  const toggleDropFilters = () => {
    filtersIsOpen.value = !filtersIsOpen.value
    document.body.style.overflow = filtersIsOpen.value ? 'hidden' : ''
  }
</script>

<style scoped lang="scss">
  .shop-header {
    display: flex;
    flex-direction: column;
    gap: 15px;
    margin-bottom: 15px;

    &__heading {
      font-size: 20px;
      font-weight: 400;
    }

    &__button {
      display: flex;
      flex-direction: row;
      gap: 10px;
      align-items: center;

      &-heading {
        font-size: 12px;
        font-weight: 400;
        color: var(--color-accent);
      }
    }
  }

  .filters {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 3;
    width: 100%;
    height: 100vh;
    padding: 16px;
    overflow-y: auto;
    background: white;

    &__header {
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 32px;

      &-heading {
        font-family: var(--font-logo);
        color: black;
      }
    }
  }
</style>
