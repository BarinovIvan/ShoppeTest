<template>
  <article class="review-card">
    <header class="review-card__header">
      <h3 class="review-card__author">{{ props.author }}</h3>
      <time class="review-card__date">6 May, 2020</time>
    </header>

    <div class="review-card__rating">
      <StarFilled v-for="star in props.rating" :key="star" />
      <StarPool v-for="star in MAX_NUMBER_OF_STARS - props.rating" :key="star" />
    </div>

    <blockquote class="review-card__content">
      {{ props.text }}
    </blockquote>
  </article>
</template>

<script setup lang="ts">
  import StarFilled from 'SvgComponents/StarFilled.vue'
  import StarPool from 'svg/SvgComponents/StarPool.vue'

  interface ReviewProps {
    author: string
    text: string
    rating: number
  }

  const props = defineProps<ReviewProps>()
  const MAX_NUMBER_OF_STARS = 5
</script>

<style scoped lang="scss">
  .review-card {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
    width: 100%;
    padding-bottom: 2.5rem;
    border-bottom: 1px solid var(--color-border);

    &:last-child {
      padding-bottom: 0;
      border-bottom: none;
    }

    &__header {
      display: flex;
      gap: 1rem;
      align-items: center;
    }

    &__author {
      margin: 0;
      font-size: var(--font-size-medium);
      font-weight: var(--font-weight-bold);
    }

    &__date {
      font-size: var(--font-size-small);
      color: var(--color-text-secondary);
    }

    &__rating {
      display: flex;
      gap: 0.6rem;
    }

    &__content {
      margin: 0;
      font-size: var(--font-size-medium);
      line-height: 1.5;
      color: var(--color-text-primary);
    }
  }
</style>
