<template>
  <div class="form-control">
    <label :for="id">{{ label }}</label>
    <textarea
      :id="id"
      :rows="rows"
      :placeholder="placeholder"
      :value="modelValue"
      @input="change"
    ></textarea>
  </div>
</template>

<script>
export default {
  emits: ["update:modelValue"],
  props: {
    modelValue: String,
    label: String,
    placeholder: String,
    rows: Number,
  },
  methods: {
    change(e) {
      this.$emit("update:modelValue", e.target.value);
    },
  },
  data() {
    return {
      id: Math.random(),
    };
  },
};
</script>

<style>
</style>