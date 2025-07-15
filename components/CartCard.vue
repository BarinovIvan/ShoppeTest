<template>
  <div class="product-card">
    <img :src="product.image" class="product-card__image" />

    <div class="product-card__content">
      <div class="product-card__info">
        <p class="product-card__title">{{ product.title }}</p>
        <p class="product-card__details">Black / Medium</p>
        <p class="product-card__price">${{ totalPrice }}</p>
      </div>
    </div>

    <QuatityCount
      class="product-card__quantity"
      :quantity="product.qty"
      :type="props.counterType"
      @increment="shoppingCart.incrementProduct(product.id)"
      @decrement="shoppingCart.decrementProduct(product.id)"
    />

    <button class="product-card__delete-button" @click="$emit('remove')">
      <Xicon2 />
    </button>
  </div>
</template>

<script setup lang="ts">
  import Xicon2 from '../assets/pictures/svg/SvgComponents/Xicon2.vue'
  import type { Product } from '~/types/product'
  import { useShoppingCart } from '../stores/ShoppingCartStore'

  interface Props {
    product: Product
    counterType: string
  }

  const props = defineProps<Props>()

  defineEmits(['increment', 'decrement', 'remove'])

  const totalPrice = computed(() => {
    return (props.product.price * props.product.qty).toFixed(2)
  })

  const shoppingCart = useShoppingCart()
</script>

<style scoped lang="scss">
  .product-card {
    position: relative;
    display: grid;
    grid-template-columns: 176px 237px auto;

    &__image {
      width: 136px;
      height: 136px;
      object-fit: cover;
    }

    &__content {
      display: flex;
      flex-direction: column;
    }

    &__info {
      display: flex;
      flex-direction: column;
      gap: 2px;
    }

    &__title {
      display: -webkit-box;
      max-width: 125px;
      overflow: hidden;
      text-overflow: ellipsis;
      -webkit-line-clamp: 2;
      font-size: 14px;
      -webkit-box-orient: vertical;
    }

    &__details {
      margin: 0;
      font-size: 14px;
      color: var(--color-text);
    }

    &__price {
      margin: 0;
      font-weight: bold;
      color: var(--color-accent);
    }

    &__delete-button {
      position: absolute;
      top: 0;
      right: 0;
      padding: 5px;
      cursor: pointer;
      background: none;
      border: none;
    }
  }

  .double-row .product-card__image {
    grid-row: span 2;
  }

  .bag-counter .product-card__quantity {
    place-self: end end;
  }

  @media (width <= 375px) {
    .product-card {
      grid-template-columns: 136px auto;
      column-gap: 8px;

      &__title {
        max-width: 100px;
        font-size: 12px;
      }

      &__details {
        font-size: 12px;
      }

      &__price {
        font-size: 12px;
      }

      &__image {
        grid-row: span 2;
      }

      &__info {
        display: flex;
        flex-direction: column;
        gap: 2px;
      }
    }
  }
</style>
