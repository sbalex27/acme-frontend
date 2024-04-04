<template>
  <div v-show="form === null">
    <div class="flex justify-center items-center h-screen">
      <url-dialog @fetched="onFetched" @urlChanged="onUrl"></url-dialog>
    </div>
  </div>
  <div v-if="form !== null">
    <div class="container mx-auto">
      <dynamic-form :form="form" :sendFormUrl="url"></dynamic-form>
    </div>
  </div>
</template>

<script>
import DynamicForm from "~/components/dynamic-form.vue";
import UrlDialog from "~/components/url-dialog.vue";

export default {
  components: {
    DynamicForm,
    UrlDialog,
  },
  data() {
    return {
      form: null,
      url: null,
    };
  },
  methods: {
    onFetched(form) {
      this.form = form;
    },
    onUrl(url) {
      this.url = url;
    },
  },
};
</script>

<style></style>
