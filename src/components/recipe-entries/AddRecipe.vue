<!--Add Recipe Page: FORM-->

<template>
  <base-dialog
    v-if="inputIsInvalid"
    title="Invalid Input"
    @close="confirmError"
  >
    <template #default>
      <p>You must fill out all fields.</p>
      <p>Please check all inputs.</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="name">Recipe Name</label>
        <input id="name" name="name" type="text" ref="nameInput" />
      </div>
      <div class="form-control">
        <label for="ingredients">Ingredients</label>
        <textarea
          id="ingredients"
          name="ingredients"
          rows="5"
          ref="ingInput"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="instructions">Instructions</label>
        <textarea
          id="instructions"
          name="instructions"
          rows="10"
          wrap="hard"
          ref="instInput"
        ></textarea>
      </div>
      <div>
        <base-button type="submit">Add Recipe</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  inject: ["addRecipe"],
  data() {
    return {
      inputIsInvalid: false,
    };
  },
  methods: {
    submitData() {
      const enteredName = this.$refs.nameInput.value.trim();
      const enteredIngredients = this.$refs.ingInput.value.trim();
      const enteredInstructions = this.$refs.instInput.value.trim();

      if (
        enteredName === "" ||
        enteredIngredients === "" ||
        enteredInstructions === ""
      ) {
        this.inputIsInvalid = true;
        return;
      }
      this.addRecipe(enteredName, enteredIngredients, enteredInstructions);

      this.$refs.nameInput.value = "";
      this.$refs.ingInput.value = "";
      this.$refs.instInput.value = "";
    },
    confirmError() {
      this.inputIsInvalid = false;
    },
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
