<template>
  <UCard class="w-1/2">
    <template #header>
      <!-- <Placeholder class="h-8" /> -->
      <h1 class="text-2xl font-bold">Cuestionario</h1>
    </template>

    <div>
      <UInput
        v-model="url"
        placeholder="Introduce la URL de la encuesta"
        class="w-full"
      ></UInput>
    </div>

    <template #footer>
      <UButton @click="submit"> Comenzar </UButton>
    </template>
  </UCard>
</template>

<script>
export default {
  data() {
    return {
      url: "https://localhost:7277/api/FormFilling/conocimientos-desarrollo-software",
    };
  },
  watch: {
    url() {
      this.$emit("urlChanged", this.url);
    },
  },
  methods: {
    async submit() {
      const response = await $fetch(this.url, {
        method: "GET",
      });

      // Emit the response to the form page
      this.$emit("fetched", response);
      this.$emit("urlChanged", this.url);
    },
  }
};
</script>

<style></style>
