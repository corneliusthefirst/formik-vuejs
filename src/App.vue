<template>
  <div id="app">
    <Formik
      :initialValues="{ name: '', email: '' }"
      :onSubmit="onSubmit"
      :validate="validate"
    >
      <template #default="{ values, errors, handleChange, handleSubmit, isSubmitting }">
        <form @submit="handleSubmit">
          <div>
            <label for="name">Name</label>
            <input
              type="text"
              name="name"
              id="name"
              :value="values.name"
              @input="handleChange"
            />
            <div v-if="errors.name">{{ errors.name }}</div>
          </div>
          <div>
            <label for="email">Email</label>
            <input
              type="email"
              name="email"
              id="email"
              :value="values.email"
              @input="handleChange"
            />
            <div v-if="errors.email">{{ errors.email }}</div>
          </div>
          <button type="submit" :disabled="isSubmitting">Submit</button>
        </form>
      </template>
    </Formik>
  </div>
</template>

<script>
import FormikVue from './components/Formik.vue';

export default {
  name: 'App',
  components: {
    Formik: FormikVue,
  },
  methods: {
    onSubmit(values) {
      console.log('onSubmit', values);
    },
    validate(values) {
      const errors = {};
      if (!values.name) {
        errors.name = 'Required';
      }
      if (!values.email) {
        errors.email = 'Required';
      } else if (!/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i.test(values.email)) {
        errors.email = 'Invalid email address';
      }
      return errors;
    },
  },
};

</script>