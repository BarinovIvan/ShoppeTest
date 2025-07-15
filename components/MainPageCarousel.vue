<template>
  <div class="carousel">
    <div v-if="errorLoading" class="carousel__container">
      <div v-if="!isLoading">
        <div class="carousel-container">
          <transition tag="div" name="slide">
            <div v-if="currentProduct" :key="currentProduct.id" class="carousel__container-card">
              <img
                class="carousel__container-photo"
                src="pictures/cover.png"
                :alt="currentProduct.title"
              />
              <div class="carousel__container-description">
                <h1 class="carousel__container-description-heading">
                  {{ currentProduct.title }}
                </h1>
                <h2 class="carousel__container-description-price">${{ currentProduct.price }}</h2>
                <ButtonComp variant="special" size="xl" @click="navigateToPage(currentProduct.id)"
                  >View product
                </ButtonComp>
              </div>
            </div>
          </transition>
        </div>

        <nav class="carousel__navigation">
          <ul>
            <li
              v-for="page in pagesNumber"
              :key="page"
              :class="{ activePage: isActive(page) }"
              @click="changePage(page)"
            />
          </ul>
        </nav>
      </div>
      <DefaultSpinner v-else />
    </div>
    <ErrorMessage v-if="!errorLoading" class="error" />
  </div>
</template>

<script lang="ts" setup>
  import ErrorMessage from './ErrorMessage.vue'
  import type { Product } from '~/types/product'
  import goToPageItem from 'composables/goToPageItem'

  onMounted(async () => {
    await fetchByURL()
    startInterval()
  })

  const { navigateToPage } = goToPageItem()

  const intervalId = ref<number | null>(null)

  const pagesNumber = 5
  const currentPage = ref(1)

  const isActive = (page: number): boolean => page === currentPage.value

  const changePage = (page: number) => {
    currentPage.value = page
    startInterval()
  }

  const startInterval = () => {
    if (intervalId.value) {
      clearInterval(intervalId.value)
    }
    intervalId.value = window.setInterval(autoChangePage, 6000)
  }

  const autoChangePage = () => {
    if (currentPage.value === pagesNumber) {
      currentPage.value = 1
    } else {
      currentPage.value = currentPage.value + 1
    }
  }

  const { isLoading, errorLoading, data, fetchByURL } = useFetch<Product[]>(
    'https://fakestoreapi.com/products',
  )

  const currentProduct = computed(() => {
    return data.value?.[currentPage.value - 1]
  })

  onUnmounted(() => {
    if (intervalId.value) {
      window.clearInterval(intervalId.value)
    }
  })
</script>

<style lang="scss" scoped>
  .carousel {
    position: relative;
    z-index: 0;
    width: 100%;
    height: 646px;
    margin-bottom: 64px;
    color: var(--color-contrast);
    border-radius: 16px;

    &__container {
      &-card {
        position: absolute;
        z-index: 2;
        display: flex;
        flex-direction: column;
        gap: 48px;
        justify-content: center;
        width: 100%;
        height: 100%;
        padding-left: 30px;
        margin-right: 200px;
      }

      &-photo {
        position: absolute;
        top: 0;
        left: 0;
        z-index: -1;
        width: 100%;
        height: 100%;
      }

      &-description {
        display: flex;
        flex-direction: column;
        gap: 16px;
        max-width: 600px;
        margin-right: auto;

        &-heading {
          font-size: clamp(1.25rem, 0.964rem + 1.221vw, 2.063rem);
        }

        &-price {
          margin-bottom: 48px;
        }
      }
    }

    &__navigation {
      position: absolute;
      bottom: 26px;
      left: 50%;
      z-index: 2;
      transform: translateX(-50%);

      & ul {
        display: flex;
        gap: 14px;
        align-items: center;
      }

      & li {
        width: 9px;
        height: 9px;
        cursor: pointer;
        background-color: var(--color-contrast);
        border-radius: 50%;
      }

      & .activePage {
        width: 16px;
        height: 16px;
        background-color: transparent;
        border: 1px solid var(--color-contrast);
        border-radius: 50%;
      }
    }
  }

  .slide-enter-active,
  .slide-leave-active {
    transition: transform 1s ease;
  }

  .slide-enter-from {
    transform: translateX(calc(100% + 96px));
  }

  .slide-leave-to {
    transform: translateX(calc(-100% - 96px));
  }

  @media (width <= 375px) {
    .carousel {
      height: 354px;
      margin-bottom: 21px;
      border-radius: 8px;

      &__container {
        &-card {
          display: flex;
          justify-content: flex-end;
          padding-bottom: 26px;
          padding-left: 8px;
        }

        &-photo {
          object-fit: cover;
          object-position: 80% 30%;
          border-radius: 8px;
        }

        &-description {
          gap: 3px;

          &-heading {
            flex-wrap: wrap;
            max-width: 217px;
          }

          &-price {
            margin-bottom: 10px;
            font-size: 14px;
            font-weight: 400;
            line-height: 26px;
          }
        }
      }

      &__navigation {
        bottom: 8px;

        & ul {
          gap: 6px;
        }

        & li {
          width: 4px;
          height: 4px;
        }

        & .activePage {
          width: 7px;
          height: 7px;
        }
      }
    }

    .slide-enter-from {
      transform: translateX(calc(100% + 16px));
    }

    .slide-leave-to {
      transform: translateX(calc(-100% - 16px));
    }
  }
</style>
