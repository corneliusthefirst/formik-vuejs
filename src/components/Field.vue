<script setup>
import {defineProps, inject} from "vue";
const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  as: {
    type: String || Object,
    default: "input",
  },
});
const data = inject("formikProvider");
const handleInput = (e) => {
  data.set(props.name, e.target.value);
}
const handleComponent = (e) => {
  data.set(props.name, e)
}
</script>

<template>
  <component v-if="typeof as === 'string'"
             :is="as" :name="name"
             :value="data.values.value[name]" @input="handleInput"/>

  <component v-else :is="as" :name="name"
             :modelValue="data.values.value[name]" v-on:update:modelValue="handleComponent"/>
</template>