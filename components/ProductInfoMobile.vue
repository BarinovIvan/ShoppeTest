<template>
  <div class="info-mobile">
    <div class="info-mobile__description">
      <transition v-if="showDescription" name="fade">
        <item-page-description :text="props.description" />
      </transition>

      <transition v-else name="fade">
        <item-page-description class="info-mobile__description-text" :text="props.description" />
      </transition>

      <button
        class="info-mobile__description-button span-accent"
        :class="{ active: showDescription }"
        @click="toggleShowDescription"
      >
        View More
        <MarkRight :class="{ 'mark-rotate': showDescription }" />
      </button>
    </div>

    <div class="info-mobile__pages">
      <div class="info-mobile__pages-item">
        <button class="info-mobile__pages-button" @click="togglePageDescription">
          <p>Description</p>
          <MarkDown class="mark-small" :class="{ 'mark-rotate': showPageDescription }" />
        </button>
        <ItemPageDescription v-if="showPageDescription" :text="props.description" />
      </div>

      <div>
        <button id="1" class="info-mobile__pages-button" @click="togglePageInfo">
          <p>Additional information</p>
          <MarkDown class="mark-small" :class="{ 'mark-rotate': showPageInfo }" />
        </button>
        <ItemPageInformation v-if="showPageInfo" />
      </div>

      <div>
        <button id="1" class="info-mobile__pages-button" @click="togglePageReviews">
          <p>Reviews({{ props.count }})</p>
          <MarkDown class="mark-small" :class="{ 'mark-rotate': showPageReviews }" />
        </button>
        <ItemPageReviews v-if="showPageReviews" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
  import MarkDown from '../assets/pictures/svg/SvgComponents/MarkDown.vue'
  import MarkRight from '../assets/pictures/svg/SvgComponents/MarkRight.vue'

  interface PageInfo {
    description: string
    count: number
  }

  const props = defineProps<PageInfo>()

  const showDescription = ref<boolean>(false)

  const showPageDescription = ref<boolean>(false)
  const showPageInfo = ref<boolean>(false)
  const showPageReviews = ref<boolean>(false)

  const toggleShowDescription = () => (showDescription.value = !showDescription.value)

  const togglePageDescription = () => {
    showPageDescription.value = !showPageDescription.value
  }

  const togglePageInfo = () => {
    showPageInfo.value = !showPageInfo.value
  }

  const togglePageReviews = () => {
    showPageReviews.value = !showPageReviews.value
  }
</script>

<style scoped lang="scss">
  .info-mobile {
    flex-direction: column;

    &__description {
      display: flex;
      flex-direction: column;
      gap: 6px;
      align-items: start;
      margin-bottom: 16px;

      &-text {
        display: -webkit-box;
        overflow: hidden;
        text-overflow: ellipsis;
        -webkit-line-clamp: 2;
        transition: all 1s ease;
        -webkit-box-orient: vertical;

        &.active {
          -webkit-line-clamp: unset;
        }
      }

      &-button {
        position: relative;
        display: flex;
        flex-direction: row;
        gap: 5px;
        align-items: center;
        margin-bottom: 14px;
        cursor: pointer;
      }
    }

    &__pages {
      display: flex;
      flex-direction: column;
      gap: 10px;
      padding: 15px 0;
      border-top: 1px solid var(--color-decorative);
      border-bottom: 1px solid var(--color-decorative);

      &-item:last-child {
        margin-bottom: 15px;
      }

      &-button {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        width: 100%;
      }
    }
  }
</style>
