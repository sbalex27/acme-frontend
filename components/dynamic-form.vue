<template>
  <div>
    <!-- Title -->
    <div class="mb-4 mt-6">
      <h1 class="text-2xl font-bold">Formulario</h1>
      <h1 class="text-1xl font-semibold">{{ form.description }}</h1>
    </div>

    <!-- Success -->
    <div
      v-if="success"
      class="bg-green-200 text-green-700 text-sm p-4 rounded-lg mb-4"
    >
      <div class="text-green-700 text-lg mb-1 font-semibold">
        Formulario Enviado
      </div>
      <div>Gracias por enviar el formulario.</div>
    </div>

    <!-- Guest Name -->
    <div class="mb-4">
      <UInput
        v-model="guestName"
        placeholder="Enviar formulario a nombre de..."
      ></UInput>
    </div>

    <!-- Errors -->
    <div
      v-if="errors !== null"
      class="bg-red-200 text-red-700 text-sm p-4 rounded-lg mb-4"
    >
      <div class="text-red-700 text-lg mb-1 font-semibold">
        Formulario Inválido
      </div>

      <ul>
        <li v-for="errorField in errors" :key="errorField">
          <div v-for="error of errorField" :key="error">
            <div>{{ error }}</div>
          </div>
        </li>
      </ul>
    </div>

    <!-- Fields -->
    <div v-for="(field, index) in form.fields" :key="field.id">
      <dynamic-field class="py-2" v-model="form.fields[index]"></dynamic-field>
    </div>

    <!-- Submit Button -->
    <div class="mt-6 flex justify-end">
      <UButton :loading="loading" @click="submitForm" :disabled="success"
        >Enviar</UButton
      >
    </div>

    <!-- Debug Info -->
    <!-- <pre class="font-mono text-xs text-gray-500">{{ resultFields }}</pre> -->
  </div>
</template>

<script>
import dynamicField from "./dynamic-field.vue";
export default {
  components: { dynamicField },
  data() {
    return {
      guestName: "",
      errors: null,
      success: false,
      loading: false,
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
      this.errors = null;

      const request = {
        filledBy: this.guestName,
        fields: this.resultFields,
      };

      this.loading = true;

      await $fetch(this.sendFormUrl, {
        method: "POST",
        body: JSON.stringify(request),
        headers: {
          "Content-Type": "application/json",
        },
      })
        .then((response) => {
          this.success = true;
        })
        .catch((err) => {
          this.errors = err.data;
        })
        .finally(() => {
          this.loading = false;
        });
    },
  },
};
</script>

<style></style>
