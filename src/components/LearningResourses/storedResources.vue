<template>
  <ul>
    <learning-resources
      v-for="lr in resources"
      :key="lr.id"
      :lr="lr"
    ></learning-resources>
  </ul>
</template>
<script>
import LearningResources from "./LearningResources.vue";

export default {
  inject: ["resources"],
  components: {
    LearningResources,
  },
};
</script>
<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
