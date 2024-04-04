<template>
  <div>
    <div v-if="isText">
      <UInput
        v-model="modelValue.value"
        :placeholder="modelValue.title"
        class="w-full"
      ></UInput>
    </div>
    <div v-else-if="isNumber">
      <UInput
        v-model="modelValue.value"
        :placeholder="modelValue.title"
        class="w-full"
        type="number"
      ></UInput>
    </div>
    <div v-else-if="isDate">
      <UInput
        v-model="modelValue.value"
        :placeholder="modelValue.title"
        class="w-full"
        type="date"
      ></UInput>
    </div>
    <div v-else-if="isBoolean">
      <UCheckbox
        v-model="modelValue.value"
        :label="modelValue.title"
      ></UCheckbox>
    </div>
    <div v-else>
      <p>Field type {{ modelValue.type }} not supported</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: Object,
      required: true,
    },
  },
  emit: ["update:modelValue"],
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
      return this.modelValue.type === "Text";
    },
    isNumber() {
      return this.modelValue.type === "Number";
    },
    isDate() {
      return this.modelValue.type === "Date";
    },
    isBoolean() {
      return this.modelValue.type === "Boolean";
    },
  },
};
</script>

<style></style>
