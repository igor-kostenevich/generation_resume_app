<template>
  <div class="avatar">
    <img :src="valueForComponent" />
  </div>
</template>

<script>
export default {
  props: {
    valueForComponent: String,
  },
};
</script>