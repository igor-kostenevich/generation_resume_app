<template>
  <div class="container column">
    <form class="card card-w30" @submit.prevent="onSubmitHandler">
      <app-select
        ref="selectRef"
        label="Выберите тип блока"
        @option-selected="onSelected"
      ></app-select>

      <app-textarea
        ref="textareaRef"
        placeholder="Введите текст"
        label="Значение"
        v-model="valueText"
        :rows="4"
      ></app-textarea>

      <app-button
        :valueText="valueText.length"
        @add-block="addBlock"
        :disabled="true"
        >Добавить</app-button
      >
    </form>

    <div class="card card-w70">
      <div v-if="blocks.length" class="blocks-wrapper">
        <component
          :is="item.nameComponent"
          v-for="item in blocks"
          :key="item"
          :valueForComponent="item.value"
        ></component>
      </div>
      <h3 v-else>Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>
  <div class="container">
    <app-loader v-if="loading"></app-loader>
    <component 
      :is="'app-comments'" 
      :comments="comments" 
      :loadComments="loadComments" 
      v-else
    ></component>
  </div>
</template>

<script>
import AppSelect from "./components/AppSelect";
import AppTextarea from "./components/AppTextarea";
import AppButton from "./components/AppButton";
import Title from "./components/elements/Title";
import Subtitle from "./components/elements/Subtitle";
import Avatar from "./components/elements/Avatar";
import Text from "./components/elements/Text";
import AppComments from "./components/AppComments";
import AppLoader from "./components/AppLoader";
import axios from "axios";

export default {
  data() {
    return {
      valueText: "",
      blocks: [],
      currentComponent: "title",
      activeSelectedValue: "title",
      comments: [],
      loading: false,
    };
  },
  computed: {},
  methods: {
    onSubmitHandler() {
      this.valueText = "";
      this.$refs.selectRef.optionDefault();
    },
    onSelected(data) {
      this.activeSelectedValue = data;
    },
    addBlock() {
      this.currentComponent = this.activeSelectedValue;
      this.blocks.push({ nameComponent: this.currentComponent, value: this.valueText  });
    },
    async loadComments() {
      this.loading = true;
      const { data } = await axios.get(
        "https://jsonplaceholder.typicode.com/comments?_limit=42"
      );
      this.comments = data;
      this.loading = false;
    },
  },

  components: {
    AppSelect,
    AppTextarea,
    AppButton,
    Title,
    Subtitle,
    Avatar,
    Text,
    AppComments,
    AppLoader,
  },
};
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
