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
  alert("Formulaire envoyé \n" + JSON.stringify(values));
}

</script>

<template >

  <h1>Custom Formik Project</h1>
  <Formik v-slot="{submit,errors, isSubmitting}" :initialValues="initialValues"
          :validate="(values) => validationSchema.validateSync(values)" @submit="onSubmit">
    <form @submit.prevent="submit">
      <div>
        <Field name="name" as="input"/>
        <button :disabled="isSubmitting" type="submit">Submit</button>
      </div>
      <div>
        <template v-for="error in errors" v-bind:key="error">
          <p style="color: #d95a5a">{{ error }}</p>
        </template>
      </div>
    </form>
  </Formik>
</template>