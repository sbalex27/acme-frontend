<template>
  <div>
    <!-- Title -->
    <h1 class="text-2xl font-bold">Formulario</h1>
    <h1 class="text-1xl font-semibold">{{form.description}}</h1>

    <!-- Fields -->
    <div v-for="field in form.fields" :key="field.id">
      <dynamic-field :field="field"></dynamic-field>
    </div>

    <!-- Debug Info -->
    <pre class="font-mono text-xs text-gray-500">{{ form }}</pre>
  </div>
</template>

<script>
import dynamicField from './dynamic-field.vue';
export default {
  components: { dynamicField },
  props: {
    form: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style></style>
