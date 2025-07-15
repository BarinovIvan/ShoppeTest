<template>
  <div>
    <NuxtLayout>
      <div class="error-container">
        <h1 class="error-container__heading">404 ERROR</h1>
        <h3 class="error-container__description">
          This page not found; <br />
          back to home and start again
        </h3>
        <button-comp size="l" variant="secondary">
          <NuxtLink to="/MainPage">Homepage</NuxtLink>
        </button-comp>
      </div>
    </NuxtLayout>
  </div>
</template>

<script setup>
  useHead({
    title: '404 - Page Not Found',
  })
</script>

<style lang="scss" scoped>
  .error-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    max-width: 400px;
    padding: 20px;
    margin: 250px auto;
    font-family: var(--font-main);
    text-align: center;

    &__heading {
      margin-bottom: 24px;
      font-size: 2.5rem;
      color: black;
    }

    &__description {
      margin-bottom: 64px;
      font-size: 1.5rem;
      color: #333;
    }
  }

  @media (width <= 375px) {
    .error-container {
      margin: 205px auto;

      &__heading {
        margin-bottom: 10px;
        font-size: var(--font-size-h4);
      }

      &__description {
        margin-bottom: 24px;
        font-size: 12px;
        font-weight: 400;
      }
    }
  }
</style>
