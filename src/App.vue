<script setup>
import * as yup from "yup";
import Formik from "./components/Formik.vue";
import Field from "./components/Field.vue";

const initialValues = {
  name: "",
};
const validationSchema = yup.object({
  name: yup.string().min(3).max(15).required(),
});

const onSubmit = (values) => {
  console.log(values);
};

</script>

<template >
  <h1>Custom Formik Project</h1>
  <Formik v-slot="{handleSubmit, errors, isSubmitting}" :initialValues="initialValues"
          :validate="() => validationSchema.validateSync(values)" @submit="onSubmit">
    <form @submit.prevent="handleSubmit">
      <div>
        <Field name="name" as="input"/>
        <br>
        <button type="submit" :disabled="isSubmitting">Submit</button>
      </div>
      <div>
        <template v-for="error in errors" v-bind:key="error">
          <p style="color: #d95a5a">{{ error }}</p>
        </template>
      </div>
    </form>
  </Formik>
</template>