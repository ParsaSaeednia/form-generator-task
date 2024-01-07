<template>
  <form @submit.prevent="submitForm">
    <div v-for="field in fields" :key="field.field" class="mb-3 w-50 mx-5">
      <label :for="field.field">{{ field.label }}</label>

      <input
          v-if="field.component === 'input'"
          :id="field.field"
          v-bind="getInputProps(field)"
          v-model="formValues[field.field]"
          :class="getInputClasses(field)"
      />

      <textarea
          v-if="field.component === 'textarea'"
          :id="field.field"
          v-bind="getInputProps(field)"
          v-model="formValues[field.field]"
          class="form-control"

      />
    </div>
    <button type="submit" class="btn btn-success mx-5">Submit</button>
  </form>
</template>

<script setup>
import { ref, watch, toRefs } from 'vue';

const props = defineProps({
  modelValue: {
    type: Object,
    default: () => ({})
  },
  fields: {
    type: Array,
    default: () => []
  }
});

const { fields } = toRefs(props);
const formValues = ref({ ...props.modelValue });

const emit = defineEmits(['update:modelValue', 'submit']);

watch(formValues, (newValue) => {
  emit('update:modelValue', newValue);
}, { deep: true });

function submitForm() {
  emit('submit', formValues.value);
}
function getInputClasses(field) {
  return field.type === 'checkbox' ? 'mx-2' : 'form-control';
}
function getInputProps(field) {
  const { component, label, ...attrs } = field;
  return attrs;
}


</script>
