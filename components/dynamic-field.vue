<template>
  <div>
    <div v-if="isText">
      <UInput
        v-model="textValue"
        :placeholder="field.title"
        class="w-full"
      ></UInput>
    </div>
    <div v-else-if="isNumber">
      <UInput
        v-model="numberValue"
        :placeholder="field.title"
        class="w-full"
        type="number"
      ></UInput>
    </div>
    <div v-else-if="isDate">
      <UInput
        v-model="dateValue"
        :placeholder="field.title"
        class="w-full"
        type="date"
      ></UInput>
    </div>
    <div v-else-if="isBoolean">
      <UCheckbox
        v-model="booleanValue"
        :label="field.title"
      ></UCheckbox>
    </div>
    <div v-else>
      <p>Field type {{ field.type }} not supported</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    field: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      textValue: null,
      numberValue: null,
      dateValue: null,
      booleanValue: null,
    };
  },
  computed: {
    isText() {
      return this.field.type === "Text";
    },
    isNumber() {
      return this.field.type === "Number";
    },
    isDate() {
      return this.field.type === "Date";
    },
    isBoolean() {
      return this.field.type === "Boolean";
    },
  },
};
</script>

<style></style>
