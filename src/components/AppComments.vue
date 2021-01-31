<template>
  <div 
    class="card" 
    v-if="comments.length"
  >
    <ul class="list">
      <li 
        class="list-item" 
        v-for="comment in comments" 
        :key="comment.id"
      >
        <div>
          <p><strong>{{ comment.email }}</strong></p>
          <small>{{ comment.body }}</small>
        </div>
      </li>
    </ul>
  </div>

  <app-button 
    :disabled="false" 
    @download="loadComments" 
    v-else
  >Загрузить комментарии</app-button>
</template>

<script>
import AppButton from "./AppButton";

export default {
  props: {
    comments: {
      type: Object,
      required: false,
      default: {},
    },
    loadComments: Function,
  },
  components: { AppButton },
};
</script>