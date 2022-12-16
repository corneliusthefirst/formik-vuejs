<template>
    <slot
        :values="values"
        :handleSubmit="handleSubmit"
        :isSubmitting="isSubmitting"
        :errors="errors"
        :set="set"
    ></slot>
</template>

<script setup>
import { ref, watch, provide, defineProps } from "vue";

const props = defineProps({
    initialValues: {
        type: Object,
        required: true,
    },
    validate: {
        type: Function,
        default: () => {},
    },
    onSubmit: {
        type: Function,
        required: true,
    },
});

const values = ref(props.initialValues);

const errors = ref([]);

const isSubmitting = ref(false);

const handleSubmit = () => {
    try {
        props.validate(values.value);
    } catch (e) {
        errors.value = e.errors;
    } finally {
        if (Object.keys(errors.value).length === 0) {
            props.onSubmit(values.value);
        }
    }
};
const set = (name, value) => {
    console.log(name, value);
    values.value = { ...values.value, [name]: value };
    errors.value = [];
};

provide("formikProvider", { set, values });

/*watch(
    () => values.value,
    (newValues) => {
        errors.value = [];
        try {
            props.validate(newValues);
        } catch (e) {
            errors.value = e.errors;
        }
    },
    { deep: true }
);*/

</script>

