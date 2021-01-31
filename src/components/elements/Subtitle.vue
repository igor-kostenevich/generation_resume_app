<template>
  <h2>{{ valueForComponent }}<slot></slot></h2>
</template>

<script>
export default {
  props: {
    valueForComponent: String,
  }
};
</script>
