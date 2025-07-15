<template>
  <transition name="slide">
    <div v-if="props.isOpen" class="shopping-cart">
      <div class="shopping-cart__header">
        <div class="shopping-cart__header-line">
          <button
            class="shopping-cart__close-button shopping-cart__close-button--left"
            @click="closeBag"
          >
            <MarkLeft />
          </button>
          <h5 class="shopping-cart__title">Shopping bag</h5>
          <button
            class="shopping-cart__close-button shopping-cart__close-button--right"
            @click="closeBag"
          >
            <ExitButton />
          </button>
        </div>

        <span class="shopping-cart__items-count">
          {{ shoppingCart.productCart.length }} items
        </span>
      </div>

      <ul v-if="shoppingCart.productCart.length !== 0" class="shopping-cart__products-list">
        <li
          v-for="(item, index) of shoppingCart.productCart"
          :key="index"
          class="shopping-cart__product-item"
        >
          <CartCard
            class="shopping-cart__card"
            :class="'double-row bag-counter'"
            :product="item"
            counter-type="small"
            @increment="shoppingCart.incrementProduct(item.id)"
            @decrement="shoppingCart.decrementProduct(item.id)"
            @remove="shoppingCart.removeProduct(item.id)"
          />
        </li>
      </ul>

      <div v-else class="shopping-cart__products-null">В корзине пусто!</div>

      <div class="shopping-cart__footer">
        <div class="shopping-cart__summary">
          <p class="shopping-cart__summary-text">
            Subtotal ({{ shoppingCart.productCart.length }} items)
          </p>
          <span class="shopping-cart__summary-total"> ${{ shoppingCart.totalPrice }} </span>
        </div>

        <NuxtLink to="/shoppingcart">
          <button-comp
            variant="secondary"
            size="xl"
            class="shopping-cart__view-cart-button"
            @click="closeBag"
            >VIEW CART
          </button-comp>
        </NuxtLink>
      </div>
    </div>
  </transition>
</template>

<script setup lang="ts">
  import ExitButton from '../assets/pictures/svg/SvgComponents/ExitButton.vue'
  import MarkLeft from '../assets/pictures/svg/SvgComponents/MarkLeft.vue'
  import { useShoppingCart } from '../stores/ShoppingCartStore'

  interface Props {
    isOpen: boolean
  }

  const props = defineProps<Props>()

  const emit = defineEmits<{
    (e: 'closeBag'): void
  }>()

  const closeBag = () => {
    emit('closeBag')
  }

  const shoppingCart = useShoppingCart()
</script>

<style scoped lang="scss">
  .shopping-cart {
    position: fixed;
    top: 0;
    right: 0;
    z-index: 3;
    display: flex;
    flex-direction: column;
    width: 360px;
    height: 100vh;
    overflow-y: auto;
    background: white;
    border-left: 1px solid var(--color-decorative);

    &__header {
      display: flex;
      flex-direction: column;
      gap: 17px;
      padding: 72px 36px 5px;
    }

    &__header-line {
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    &__title {
      margin: 0;
      font-size: 16px;
      font-weight: 400;
      line-height: 27px;
    }

    &__items-count {
      font-size: 14px;
      color: var(--color-text);
    }

    &__close-button {
      padding: 0;
      cursor: pointer;
      background: none;
      border: none;

      &--right {
        margin-left: auto;
      }

      &--left {
        display: none;
      }
    }

    &__products-list {
      display: flex;
      flex-direction: column;
      gap: 20px;
      padding: 0 36px 24px;
      margin-bottom: 138px;
      list-style: none;
    }

    &__products-null {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100%;
      padding: 0 36px 24px;
    }

    &__product-item {
      &:last-child {
        border-bottom: none;
      }
    }

    &__footer {
      position: fixed;
      right: 0;
      bottom: 0;
      display: flex;
      flex-direction: column;
      gap: 21px;
      width: 360px;
      padding: 21px 36px 24px;
      background-color: white;
      border: 1px solid var(--color-decorative);
    }

    &__summary {
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    &__summary-text {
      margin: 0;
      font-size: 14px;
    }

    &__summary-total {
      font-weight: bold;
    }

    &__view-cart-button {
      width: 100%;
    }

    &__card {
      display: grid;
      grid-template-rows: auto auto;
      grid-template-columns: 136px auto;
      gap: 8px;

      &:first-child {
        grid-row: span 2;
      }
    }
  }

  @media (width <= 375px) {
    .shopping-cart {
      width: 100%;
      border-left: none;

      &__header {
        padding: 16px 16px 3px;
      }

      &__title {
        margin: 0 auto;
      }

      &__close-button {
        &--left {
          display: block;
        }

        &--right {
          display: none;
        }
      }

      &__items-count {
        font-size: 12px;
      }

      &__products-list {
        padding: 0 16px 16px;
        border-bottom: none;
      }

      &__footer {
        width: 100%;
        padding: 24px 12px 36px;
      }
    }
  }
</style>
