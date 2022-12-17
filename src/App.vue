<script setup>
import * as Yup from "yup";
import Formik from "@/components/Formik.vue";
import Field from "@/components/Field.vue";

const initialValues = {
  name: "",
  email: "",
};
const validationSchema = Yup.object({
  name: Yup.string().min(3).max(15).required(),
  email: Yup.string().email().required(),
});

const onSubmit = (values) => {
  alert(JSON.stringify(values, null, 2));
};

</script>

<template>
  <h1>Custom Formik Project</h1>
  <Formik v-slot="{handleSubmit, errors, isSubmitting}" :initialValues="initialValues"
          :validate="(values) => validationSchema.validateSync(values)" @submit="onSubmit">
    <form @submit.prevent="handleSubmit">
      <div>
        <Field name="name" as="input"/>
        <br>
        <Field name="email" as="input"/>
        <br>
        <button :disabled="isSubmitting" type="submit">Submit</button>
      </div>
      <div v-if="errors" style="color: red">
        <p v-for="error in errors" v-bind:key="error">{{error}}</p>
      </div>
    </form>
  </Formik>
</template>
