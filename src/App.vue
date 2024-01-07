<template>
  <FormGenerator v-model="object" :fields="schema" @submit="handleSubmit" />
</template>

<script setup>
import { ref } from 'vue';
import FormGenerator from './components/FormGenerator.vue';

// Import FormGenerator...

const object = ref({
  name: 'Alex',
  dateOfBirth: '1989-01-06', // Use an ISO date format
  eyeColor: 'blue',
  bio: 'I love apples',
  check: 'off',
});

const schema = [
  {
    field: 'name',
    label: 'Full Name',
    component: 'input',
    type: 'text',
    placeholder: 'Your Name',
  },
  {
    field: 'dateOfBirth',
    label: 'Date of Birth',
    component: 'input',
    type: 'date', // Use 'date' for the native HTML date picker
  },
  {
    field: 'eyeColor',
    label: 'Eye Color',
    component: 'input',
    type: 'text',
  },
  {
    field: 'bio',
    label: 'Biography',
    component: 'textarea',
    rows:'4'
  },
  {
    field: 'check',
    label: 'check',
    component: 'input',
    type: 'checkbox'
  },
];

function handleSubmit(formState) {
  console.log('Form submitted:', formState);
  // Handle the submitted data
}

</script>
