<template>
  <div class="form-control">
    <label :for="id">{{ label }}</label>
    <select :id="id" v-model="option">
      <option 
        v-for="item in options" 
        :key="item" 
        :value="item.value"
        :click="isActiveOption(item)"
      >
        {{ item.name }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    label: String,
  },
  methods: {
    optionDefault() {
      this.option = 'title'
    },
    isActiveOption(item){
      if(item.value === this.option){
        this.$emit('option-selected', item.value) 
      }
    }
  },
  data() {
    return {
      options: [
        { name: "Заголовок", value: "title"},
        { name: "Подзаголовок", value: "subtitle" },
        { name: "Аватар", value: "avatar"},
        { name: "Текст", value: "text"}
      ],
      option: "title",
      id: Math.random()
    };
  }
};
</script>

<style>
</style>