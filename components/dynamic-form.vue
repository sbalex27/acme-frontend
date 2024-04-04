<template>
  <div>
    <!-- Title -->
    <div class="mb-4 mt-6">
      <h1 class="text-2xl font-bold">Formulario</h1>
      <h1 class="text-1xl font-semibold">{{ form.description }}</h1>
    </div>

    <!-- Guest Name -->
    <div class="mb-4">
      <UInput
        v-model="guestName"
        placeholder="Enviar formulario a nombre de..."
      ></UInput>
    </div>

    <!-- Fields -->
    <div v-for="(field, index) in form.fields" :key="field.id">
      <dynamic-field class="py-2" v-model="form.fields[index]"></dynamic-field>
    </div>

    <!-- Submit Button -->
    <div class="mt-6 flex justify-end">
      <UButton
        @click="submitForm"
        >Enviar</UButton
      >
    </div>

    <!-- Debug Info -->
    <pre class="font-mono text-xs text-gray-500">{{ resultFields }}</pre>
  </div>
</template>

<script>
import dynamicField from "./dynamic-field.vue";
export default {
  components: { dynamicField },
  data() {
    return {
      guestName: "",
    };
  },
  props: {
    form: {
      type: Object,
      required: true,
    },
    sendFormUrl: {
      type: String,
      required: true,
    },
  },
  computed: {
    resultFields() {
      return this.form.fields.map((field) => {
        return {
          name: field.name,
          value: field.value || null,
        };
      });
    },
  },
  methods: {
    async submitForm() {
      const request = {
        filledBy: this.guestName,
        fields: this.resultFields,
      };

      const response = await $fetch(this.sendFormUrl, {
        method: "POST",
        body: JSON.stringify(request),
        headers: {
          "Content-Type": "application/json",
        },
      });

      console.log(response);
    },
  },
};
</script>

<style></style>
