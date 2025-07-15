<template>
  <div class="password-reset">
    <h1 class="password-reset__heading password-reset__heading--desktop">
      Have you Forgotten Your Password?
    </h1>
    <h1 class="password-reset__heading password-reset__heading--mobile">Lost password</h1>

    <div class="password-reset__content">
      <p class="password-reset__description password-reset__description--desktop">
        If you've forgotten your password, enter your e-mail address and we'll send you an e-mail
      </p>

      <p class="password-reset__description password-reset__description--mobile">
        If you've forgotten your password, enter your e-mail address and we'll send you an e-mail
      </p>

      <form class="password-reset__form" @submit.prevent="handleSubmit">
        <default-text-input
          v-model="form.email"
          size="medium"
          placeholder="Email"
          class="password-reset__input"
          type="email"
          :class="{ 'contacts__input--error': errors.email }"
          :error="errors.email"
          @blur="handleBlur('email')"
        />
        <button-comp size="xl" variant="primary" type="submit" class="password-reset__submit">
          RESET PASSWORD
        </button-comp>
      </form>
    </div>

    <DefaultNotification
      :isOpen="isModalOpen"
      :status="status"
      :message="message"
      button-type="close"
      @close="modalClose"
    />
  </div>
</template>

<script setup lang="ts">
  import useFormValidation from 'composables/useFormValidation'
  import useFormSubmit from 'composables/useFormSubmit'

  const { form, errors, validateForm, handleBlur, resetForm } = useFormValidation({
    email: '',
  })

  const type = 'resetPassword'

  const { submitForm, isModalOpen, status, modalClose, message } = useFormSubmit()

  const handleSubmit = () => {
    submitForm(
      'We were sent a new password to your email address.',
      'Form has errors. Please check your email address.',
      form,
      type,
      validateForm,
      resetForm,
      saveToLocalStorage,
    )
  }
</script>

<style scoped lang="scss">
  .password-reset {
    &__heading {
      margin-bottom: 40px;
      text-align: center;

      &--mobile {
        display: none;
        margin-bottom: 16px;
        font-size: 20px;
        font-weight: 400;
      }
    }

    &__content {
      display: flex;
      flex-direction: column;
      max-width: 500px;
      margin: 0 auto 250px;
    }

    &__description {
      margin-bottom: 76px;
      text-align: center;

      &--mobile {
        display: none;
        margin-bottom: 64px;
        font-size: 12px;
        line-height: 20px;
      }
    }

    &__form {
      display: flex;
      flex-direction: column;
      gap: 64px;
    }

    &__submit {
      font-size: 16px;
      font-weight: 700;
    }
  }

  @media (width <= 375px) {
    .password-reset {
      &__heading {
        &--desktop {
          display: none;
        }

        &--mobile {
          display: block;
        }
      }

      &__description {
        &--desktop {
          display: none;
        }

        &--mobile {
          display: flex;
          text-align: left;
        }
      }

      &__content {
        margin-bottom: 94px;
      }
    }
  }
</style>
