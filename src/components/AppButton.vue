<template>
  <button
    class="btn primary"
    @click="$emit('add-block'), $emit('download')"
    :disabled="disabledBbtn"
  >
    <slot></slot>
  </button>
</template>

<script>
export default {
  emits: ["add-block", "download"],
  props: {
    valueText: Number,
    disabled: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      isDisable: true,
    };
  },
  computed: {
    disabledBbtn() {
      if (this.isDisable === this.disabled) {   // Сделал условие на проверку символов в textarea внутри компонента кнопки
        return this.disabled                    // Не знаю правильно ли, но условие в одну строчку в computed в App файле  
      }                                         // мне показалось слишком легким, да и по идее эту логику нужно выносить в
        return false                            // компонент, к которому она пренадлежит. Однако мой вариант мне кажется слишком
    }                                           // заморочным, нужно теперь на каждую кнопку биндить disabled во всем приложении,                                                                                 
                                                // да и функция далеко не универсальна. Вопрос в следующем, можно ли как-то получать
  },                                            // реактивно данные, например количество символов в текстареа, в другом компоненте?
  watch: {                                      // Возможно я не до конца понял и это было в видео уроках, тыкните пожалуйста)
    valueText(value) {                          
      if (value >= 4) {                         
        this.isDisable = false;
      } else {
        this.isDisable = true;
      }
    },
  },
};
</script>

<style>
</style>