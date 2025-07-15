<template>
  <div class="shopping-cart">
    <h1 class="shopping-cart__header">Shopping cart</h1>
    <div v-if="cartLength" class="shopping-cart__container">
      <div class="shopping-cart__view">
        <ul class="shopping-cart__list">
          <li
            v-for="item in shoppingCart.productCart"
            :key="item.id"
            class="shopping-cart__list-item"
          >
            <CartCard
              :class="'bag-counter'"
              :product="item"
              counter-type="big"
              @increment="shoppingCart.incrementProduct(item.id)"
              @decrement="shoppingCart.decrementProduct(item.id)"
              @remove="shoppingCart.removeProduct(item.id)"
            />
          </li>
        </ul>

        <DefaultCouponAdd />
      </div>

      <div class="shopping-cart__totals">
        <div class="shopping-cart__description">
          <h2 class="shopping-cart__totals-heading">Cart totals</h2>
          <div class="shopping-cart__totals-info totals-info">
            <h5 class="totals-info__text">SUBTOTAL</h5>
            <h5 class="totals-info__text">$ {{ shoppingCart.totalPrice }}</h5>
            <h5 class="totals-info__text">SHIPPING</h5>
            <span class="totals-info__text"
              >Shipping costs will be calculated once you have provided address.
            </span>
          </div>

          <div class="totals-info__total">
            <span class="totals-info__text">TOTAl</span>
            <span class="totals-info__text">${{ shoppingCart.totalPrice }}</span>
          </div>
        </div>

        <NuxtLink to="/checkout">
          <button-comp variant="primary" size="xl">PROCEED TO CHECKOUT </button-comp>
        </NuxtLink>
      </div>
    </div>

    <div v-else class="shopping-cart__null">
      <p>В корзине пусто!</p>
      <NuxtLink to="/shop">
        <button-comp variant="primary" size="xl">TO SHOP</button-comp>
      </NuxtLink>
    </div>
  </div>
</template>

<script setup lang="ts">
  import { useShoppingCart } from '../stores/ShoppingCartStore'
  import CartCard from '../components/CartCard.vue'
  import DefaultCouponAdd from '../components/DefaultCouponAdd.vue'

  const shoppingCart = useShoppingCart()

  const cartLength = computed(() => {
    return shoppingCart.productCart.length !== 0
  })
</script>

<style scoped lang="scss">
  .shopping-cart {
    display: flex;
    flex-direction: column;
    margin-bottom: 200px;

    &__header {
      margin: 0 auto 64px;
    }

    &__container {
      display: flex;
      flex-direction: row;
      justify-content: space-between;
    }

    &__null {
      display: flex;
      flex-direction: column;
      gap: 30px;
      align-items: center;
    }

    &__view {
      display: flex;
      flex-direction: column;
      gap: 156px;
      width: 580px;
    }

    &__list {
      display: flex;
      flex-direction: column;
      gap: 40px;
      max-width: 570px;

      &-item {
        width: 100%;
        padding-bottom: 40px;
        border-bottom: 1px solid #e4e4e4;
      }
    }

    &__description {
      display: flex;
      flex-direction: column;
      gap: 25px;
      justify-content: start;
      max-width: 460px;
      padding: 15px 15px 20px;
      margin-bottom: 24px;
      background-color: #e4e4e4;
      border-radius: 4px;
    }
  }

  .totals-info {
    display: grid;
    grid-template-columns: auto auto;
    gap: 28px 128px;
    width: 100%;
    padding-bottom: 23px;
    border-bottom: 1px solid var(--color-decorative);

    &__total {
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: space-between;
    }
  }

  @media (width <= 375px) {
    .shopping-cart {
      margin-bottom: 96px;

      &__header {
        margin: 0;
        margin-right: auto;
        margin-bottom: 16px;
        font-size: 16px;
        font-weight: 400;
      }

      &__container {
        flex-direction: column;
      }

      &__view {
        gap: 24px;
        width: 100%;
        margin-bottom: 45px;
      }

      &__list {
        gap: 22px;

        &-item {
          width: 100%;
          padding-bottom: 0;
          border-bottom: none;
        }
      }

      &__totals {
        gap: 25px;

        &-heading {
          font-size: 16px;
        }
      }
    }

    .totals-info {
      column-gap: 45px;

      &__text {
        font-size: 12px;
      }
    }
  }
</style>
