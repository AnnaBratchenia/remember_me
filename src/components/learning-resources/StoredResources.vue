<template>
  <ul>
    <learning-resources
      v-for="res in resources"
      v-bind:key="res.id"
      v-bind:id="res.id"
      v-bind:title="res.title"
      v-bind:description="res.description"
      v-bind:link="res.link"
    ></learning-resources>
  </ul>
</template>
<script>
import LearningResources from "./LearningResources.vue";
export default {
  components: { LearningResources },
  inject: ["resources"],
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
