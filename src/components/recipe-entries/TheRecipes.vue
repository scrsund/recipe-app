<!--DATA/LOGIC for UI-->

<template>
  <base-card>
    <!--displaying the UI through 'stored-recipes' tag from StoredRecipes.app-->
    <base-button
      @click="setSelectedTab('stored-recipes')"
      :mode="storeRecipeButtonMode"
      >Recipe List</base-button
    >
    <base-button
      @click="setSelectedTab('add-recipe')"
      :mode="addRecipeButtonMode"
      >Add Recipe</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredRecipes from "./StoredRecipes.vue";
import AddRecipe from "./AddRecipe.vue";

export default {
  components: {
    StoredRecipes,
    AddRecipe,
  },
  data() {
    return {
      selectedTab: "stored-recipes",
      storedRecipes: [
        {
          id: "sugarcake",
          recipeName: "Sugar Cake",
          ingredients: [
            "2 dl sugar",
            "2 eggs",
            "2 dl and a 3rd of flour",
            "2 heaping tsp Vanilla powder",
            "2 tsp baking powder",
            "1 dl milk",
            "1/2 dl butter (melted)",
          ],
          instructions:
            "Heat the oven to 175 C. Wisp sugar and eggs until kind of fluffy. Wisp everything else together. Bake for 20 - 30 minutes. Check every 5th minute after 20 minutes. Do yo thang.",
        },
        {
          id: "scones",
          recipeName: "Scones",
          ingredients: [
            "4 dl flour",
            "2 tsp baking powder",
            "2 pinch salt",
            "50g butter",
            "2 dl milk",
          ],
          instructions:
            "Heat oven to 250 C. Mix flour, baking powder, and salt in a bowl. Add butter and milk. Bake for 10-12 minutes. Eat everything. Leave nothing behind.",
        },
      ],
    };
  },
  computed: {
    storeRecipeButtonMode() {
      return this.selectedTab === "stored-recipes" ? null : "flat";
    },
    addRecipeButtonMode() {
      return this.selectedTab === "add-recipe" ? null : "flat";
    },
  },
  provide() {
    return {
      recipes: this.storedRecipes,
      addRecipe: this.addRecipe,
      deleteRecipe: this.deleteRecipe,
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addRecipe(recipeName, ingredients, instructions) {
      const ingredientsArray = ingredients
        .split("\n")
        .map((ingredient) => ingredient.trim());

      const newRecipe = {
        id: new Date().toISOString(),
        recipeName: recipeName,
        ingredients: ingredientsArray,
        instructions: instructions,
      };
      this.storedRecipes.unshift(newRecipe);
      this.selectedTab = "stored-recipes";
    },
    deleteRecipe(recipeId) {
      const recipeIndex = this.storedRecipes.findIndex(
        (recipe) => recipe.id === recipeId
      );
      this.storedRecipes.splice(recipeIndex, 1);
    },
  },
};
</script>
