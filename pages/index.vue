<template>
  <div class="flex justify-center items-center h-screen">
    <UCard class="w-1/3">
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
  </div>
</template>

<script>
export default {
  data() {
    return {
      url: "",
    };
  },
  methods: {
    async submit() {
      const response = await $fetch(this.url, {
        method: "GET",
      });
      console.log(response);
      //   this.$router.push({ name: "survey", params: { url: this.url } });
    },
  },
};
</script>

<style></style>
