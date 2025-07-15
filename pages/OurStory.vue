<template>
  <div class="about">
    <div class="about__description">
      <div class="about__headings">
        <h1>About</h1>
        <h3>Who we are and why we do what we do!</h3>
      </div>
      <p class="about__text">Hello world</p>
    </div>

    <div class="about__card">
      <h2 class="about__card-heading">Top trends</h2>
      <img src="assets/pictures/OurStory/Img_01.webp" class="about__card-image" />
      <p class="about__card-text">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam placerat, augue a volutpat
        hendrerit, sapien tortor faucibus augue, a maximus elit ex vitae libero. Sed quis mauris
        eget arcu facilisis consequat sed eu felis.
      </p>
      <ul>
        <li>consectetur adipiscing elit. Aliquam placerat</li>
        <li>Lorem ipsum dolor sit amet consectetur</li>
      </ul>
    </div>

    <div class="about__card">
      <h2 class="about__card-heading">Produced with care</h2>
      <img src="assets/pictures/OurStory/Img_02.webp" class="about__card-image" />
      <p class="about__card-text">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam placerat, augue a volutpat
        hendrerit, sapien tortor faucibus augue, a maximus elit ex vitae libero. Sed quis mauris
        eget arcu facilisis consequat sed eu felis. Nunc sed porta augue. Morbi porta tempor odio,
        in molestie diam bibendu.
      </p>
    </div>
  </div>
</template>

// HTML // CSS

<style lang="scss" scoped>
  .about {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-paragraph);
    max-width: 670px;
    margin: 0 auto 250px;

    &__headings {
      display: flex;
      flex-direction: column;
      gap: 24px;
      align-items: center;
    }

    &__description {
      display: flex;
      flex-direction: column;
      gap: 46px;
      margin-bottom: 39px;
    }

    &__card {
      display: flex;
      flex-direction: column;
      margin-bottom: 39px;

      &-text {
        margin-bottom: 16px;
      }

      ul {
        margin-left: 15px;
        line-height: var(--line-height-h5);
        list-style-type: disc;
      }

      li {
        margin-left: 15px;
      }

      &-heading {
        margin-bottom: 23px;
      }

      &-image {
        max-width: 300px;
        max-height: 300px;
        margin: 48px auto;
      }
    }

    &__text {
      font-size: var(--font-size-text-large);
      font-weight: var(--font-weight-regular);
      line-height: var(--line-height-h5);
    }
  }
</style>
