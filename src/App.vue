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
      <div v-if="isActive" class="blocks-wrapper">
        <!-- <li v-for="item in blocks" :key="item">{{item}}</li> -->
     
          <component
            :is="item.value"
            v-for="(item) in blocks"
            :key="item.name"
            :valueForComponent="item.name"
          ></component>
  
      </div>
      <h3 v-else>Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>
  <!-- <div class="container">
    <p>
      <app-button
        
      >Загрузить комментарии</app-button>
    </p>
    <div class="card">
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item">
          <div>
            <p><strong>test@microsoft.com</strong></p>
            <small
              >Lorem ipsum dolor sit amet, consectetur adipisicing elit.
              Eligendi, reiciendis.</small
            >
          </div>
        </li>
      </ul>
    </div>
    <div class="loader"></div>
  </div> -->
</template>

<script>
import AppSelect from "./components/AppSelect";
import AppTextarea from "./components/AppTextarea";
import AppButton from "./components/AppButton";
import Title from "./components/elements/Title";
import Subtitle from "./components/elements/Subtitle";
import Avatar from "./components/elements/Avatar";
import Text from "./components/elements/Text";

export default {
  data() {
    return {
      valueText: "",
      isActive: false,
      blocks: [],
      currentComponent: "title",
      activeSelectedValue: "title",
    };
  },
  computed: {
    // currentProps() {
    //   if(this.currentComponent === 'Title'){
    //     // return console.log('this is title')
    //     // return 'Title'
    //   }
    // }
  },
  methods: {
    onSubmitHandler() {
      this.valueText = "";
      this.isActive = true;
      this.$refs.selectRef.optionDefault();
    },
    onSelected(data) {
      this.activeSelectedValue = data;
    },
    addBlock() {
      this.currentComponent = this.activeSelectedValue
      this.blocks.push({name: this.valueText, value: this.currentComponent});
      // console.log(this.activeSelectedValue);
      // console.log(this.valueText);
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
