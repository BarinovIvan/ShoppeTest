<template>
  <article class="product-card">
    <div class="product-card__image-wrapper">
      <img
        :src="product.image"
        :alt="product.title"
        class="product-card__image"
        @click="navigateToPage(product.id)"
      />

      <button class="product-card__overlay" @click="AddToCart(product)">ADD TO CART</button>
    </div>
    <div class="product-card__info">
      <h3 class="product-card__title">{{ product.title }}</h3>
      <span class="product-card__price">$ {{ product.price }}</span>
    </div>

    <DefaultNotification
      button-type="tocart"
      :isOpen="isModalOpen"
      :status="status"
      :message="message"
      @close="modalClose"
    />
  </article>
</template>

<script setup lang="ts">
  import { useShoppingCart } from '../stores/ShoppingCartStore'
  import type { Product } from '~/types/product'
  import goToPageItem from 'composables/goToPageItem'

  const { isModalOpen, status, modalClose, modalOpen, message } = useNotification()

  defineProps<{
    product: Product
  }>()

  const AddToCart = (product: Product) => {
    shoppingCart.addToCart(product)
    message.value = 'The item added to your Shopping bag.'
    modalOpen({ message: 'The item added to your Shopping bag.', duration: 2000 })
  }

  const { navigateToPage } = goToPageItem()

  const shoppingCart = useShoppingCart()
</script>

<style lang="scss" scoped>
  .product-card {
    display: flex;
    flex-direction: column;
    gap: 24px;
    cursor: pointer;

    &__image-wrapper {
      position: relative;
      aspect-ratio: 1 / 1;
      overflow: hidden;
      background: #f5f5f5;
      border-radius: 8px;
    }

    &__image {
      width: 100%;
      height: 100%;
      aspect-ratio: 1 / 1;
      object-fit: cover;
      transition: transform 0.3s ease;
    }

    &__overlay {
      position: absolute;
      right: 0;
      bottom: 0;
      left: 0;
      display: flex;
      visibility: hidden;
      align-items: center;
      justify-content: center;
      padding: 15px;
      font-weight: var(--font-weight-bold);
      color: black;
      pointer-events: all;
      cursor: pointer;
      background: rgb(216 216 216 / 50%);
      border: none;
      opacity: 1;
      transform: translateY(100%);
      transition: all 0.3s ease;
    }

    &__info {
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    &__title {
      display: -webkit-box;
      margin: 0;
      overflow: hidden;
      text-overflow: ellipsis;
      -webkit-line-clamp: 2;
      font-size: clamp(0.875rem, 0.768rem + 0.536vw, 1.25rem);
      line-height: var(--line-height-h3);
      -webkit-box-orient: vertical;
    }

    &__price {
      font-size: clamp(0.75rem, 0.607rem + 0.714vw, 1.25rem);
      color: var(--color-accent);
    }

    &:hover &__overlay {
      visibility: visible;
      transform: translateY(0);
    }

    &:hover &__image {
      transform: scale(1.05);
    }
  }

  @media (width <= 376px) {
    .product-card {
      gap: 6px;

      &__info {
        gap: 4px;
      }

      &__title {
        line-height: var(--line-height-body-small);
      }

      &__overlay {
        padding: 5px;
      }

      &:hover &__overlay {
        visibility: visible;
        opacity: 1;
        transform: translateY(0);
      }
    }
  }
</style>
