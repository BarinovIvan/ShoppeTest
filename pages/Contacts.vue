<template>
  <div class="contacts">
    <div class="contacts__info">
      <h1 class="contacts__title">Contact us</h1>
      <h3 class="contacts__subtitle">
        Say Hello send us your thoughts about our products or share your ideas with our Team!
      </h3>
    </div>

    <form class="contacts__form" @submit.prevent="handleSubmit">
      <div class="contacts__form-grid">
        <DefaultTextInput
          id="firstname"
          v-model="form.firstName"
          size="medium"
          placeholder="First name"
          :class="{ 'contacts__input--error': errors.firstName }"
          :error="errors.firstName"
          @blur="handleBlur('firstName')"
        />

        <DefaultTextInput
          id="lastname"
          v-model="form.lastName"
          size="medium"
          placeholder="Last name"
          :class="{ 'contacts__input--error': errors.lastName }"
          :error="errors.lastName"
          @blur="handleBlur('lastName')"
        />

        <DefaultTextInput
          v-model="form.email"
          size="medium"
          placeholder="Email"
          :class="{ 'contacts__input--error': errors.email }"
          :error="errors.email"
          @blur="handleBlur('email')"
        />

        <DefaultSelect
          v-model="selectedSubject"
          :class="{ 'contacts__select--error': errors.subject }"
          :error="errors.subject"
        />

        <DefaultTextInput
          id="message"
          v-model="form.message"
          size="medium"
          placeholder="Message"
          :class="{ 'contacts__input--error': errors.message }"
          :error="errors.message"
          @blur="handleBlur('message')"
        />
      </div>

      <ButtonComp type="submit" variant="primary" size="xl" class="contacts__submit">
        SEND
      </ButtonComp>
    </form>

    <DefaultNotification
      :isOpen="isModalOpen"
      :status="status"
      button-type="close"
      :message="message"
      @close="modalClose"
    />
  </div>
</template>

<script lang="ts" setup>
  import useFormValidation from 'composables/useFormValidation'
  import useFormSubmit from 'composables/useFormSubmit'
  import DefaultSelect from '../components/DefaultSelect.vue'

  const selectedSubject = ref('')

  const { form, errors, handleBlur, validateForm, resetForm } = useFormValidation({
    firstName: '',
    lastName: '',
    email: '',
    subject: '',
    message: '',
  })

  watch(selectedSubject, (newVal) => {
    form.subject = newVal
  })

  const type = 'contacts'

  const { submitForm, isModalOpen, status, modalClose, message } = useFormSubmit()

  const handleSubmit = () => {
    submitForm(
      'Your message has been sent successfully.',
      'Form has errors. Please check all fields.',
      form,
      type,
      validateForm,
      resetForm,
      saveToLocalStorage,
    )
  }
</script>

<style lang="scss" scoped>
  .contacts {
    display: flex;
    flex-direction: column;
    gap: 108px;
    max-width: 908px;
    margin: auto;
    margin-bottom: 250px;

    &__info {
      display: flex;
      flex-direction: column;
      gap: 39px;
      align-items: center;
      max-width: 560px;
      margin: auto;
    }

    &__title {
      font-size: 2rem;
      color: var(--color-primary);
    }

    &__subtitle {
      font-weight: normal;
      color: var(--color-text-secondary);
      text-align: center;
    }

    &__form {
      display: flex;
      flex-direction: column;
      gap: 96px;
      align-items: center;
    }

    &__form-grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 94px 116px;
      align-items: end;
      width: 100%;

      & > *:last-child {
        grid-column: span 2;
      }
    }

    &__input--error {
      border-color: var(--color-error);
    }

    &__select--error {
      :deep(.select__control) {
        border-color: var(--color-error);
      }
    }

    &__submit {
      width: 100%;
    }

    @media (width <= 376px) {
      display: flex;
      gap: 48px;
      justify-content: start;
      margin-bottom: 96px;

      &__info {
        align-items: flex-start;
        width: 100%;
      }

      &__title {
        font-size: 20px;
        font-weight: 400;
        line-height: 26px;
      }

      &__form {
        gap: 24px;
      }

      &__form-grid {
        grid-template-columns: 1fr;
        row-gap: 47px;

        & > *:last-child {
          grid-column: span 1;
        }
      }

      &__subtitle {
        display: none;
      }
    }
  }
</style>
