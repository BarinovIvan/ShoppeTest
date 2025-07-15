<template>
  <div class="error">
    <h1>Что-то пошло не так...</h1>
    <h3>Проверьте подключение к интернету!</h3>
  </div>
</template>

<style lang="scss" scoped>
  .error {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 2;
    display: flex;
    flex-direction: column;
    gap: 20px;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    color: black;
    background-color: antiquewhite;
    border-radius: 16px;
  }
</style>
