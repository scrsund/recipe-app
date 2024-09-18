<!--INFO-->

<template>
  <ul>
    <recipe-entry
      v-for="recipe in recipes"
      :key="recipe.id"
      :id="recipe.id"
      :title="recipe.recipeName"
      :ingredients="recipe.ingredients"
      :instructions="recipe.instructions"
    ></recipe-entry>
  </ul>
</template>

<script>
import RecipeEntry from "./RecipeEntry.vue";

export default {
  inject: ["recipes"],
  components: {
    RecipeEntry,
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
