<template>
  <div class="answers">
    <ReviewCard
      v-for="item of visibleReviews"
      :author="item.author"
      :text="item.text"
      :rating="item.rating"
      class="answers__item"
    />

    <ButtonComp v-if="hasMoreReviews" variant="primary" size="l" @click="loadMore">
      More
    </ButtonComp>
  </div>
</template>

<script setup lang="ts">
  import { useReviewsStore } from '../stores/ReviewsStore'

  const reviewsStore = useReviewsStore()

  const localArray = computed(() => reviewsStore.reviewsArray)

  const visibleCount = ref(3)
  const itemsPerLoad = 3

  const visibleReviews = computed(() => localArray.value.slice(0, visibleCount.value))

  const hasMoreReviews = computed(() => visibleCount.value < localArray.value.length)

  const loadMore = () => {
    visibleCount.value += itemsPerLoad
  }
</script>

<style scoped lang="scss">
  .answers {
    display: flex;
    flex-direction: column;
    gap: 24px;

    &__item {
      display: flex;
      flex-direction: column;
      width: 100%;
      padding-bottom: 39px;
      border-bottom: 1px solid var(--color-decorative);

      &:last-child {
        margin-bottom: 0;
        border-bottom: none;
      }
    }

    &__item-header {
      display: flex;
      flex-direction: row;
      gap: 16px;
      align-items: center;
      margin-bottom: 16px;
    }

    &__item-author {
      margin: 0;
    }

    &__item-date {
      font-size: var(--font-size-text-medium);
      font-weight: var(--font-weight-regular);
      color: var(--color-text);
    }

    &__item-rating {
      display: flex;
      flex-direction: row;
      gap: 10px;
      margin-bottom: 24px;
    }

    &__item-text {
      margin: 0;
      font-weight: var(--font-weight-regular);
      color: var(--color-text);
    }
  }
</style>
