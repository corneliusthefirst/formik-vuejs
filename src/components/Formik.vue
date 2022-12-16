<template>
    <div>
        <slot
            :values="values"
            :errors="errors"
            :handleChange="handleChange"
            :handleSubmit="handleSubmit"
            :isSubmitting="isSubmitting"
        ></slot>
    </div>
</template>

<script>
import { reactive, ref } from 'vue';

export default {
    props: {
        initialValues: {
            type: Object,
            required: true,
        },
        onSubmit: {
            type: Function,
            required: true,
        },
        validate: {
            type: Function,
            required: false,
        },
    },
    setup(props) {
        const values = reactive(props.initialValues);
        const errors = reactive({});
        const isSubmitting = ref(false);

        const handleChange = (e) => {
            const { name, value } = e.target;
            values[name] = value;
        };

        const handleSubmit = async (e) => {
            e.preventDefault();
            isSubmitting.value = true;
            errors.value = await props.validate(values);
            if (Object.keys(errors.value).length === 0) {
                await props.onSubmit(values);
            }
            isSubmitting.value = false;
        };

        return {
            values,
            errors,
            handleChange,
            handleSubmit,
            isSubmitting,
        };
    },
};

</script>