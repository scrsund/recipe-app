<!--DISPLAY-->

<template>
  <li>
    <base-card>
      <header>
        <h3>{{ title }}</h3>
        <base-button mode="flat" @click="deleteRecipe(id)">Delete</base-button>
      </header>
      <div>
      <p>
        <ul>
        <li v-for="ingredient in ingredients" :key="ingredient">
          {{ ingredient }}
        </li>
        </ul>
      </p>
      </div>
      <div>
      <p>{{ instructions }}</p>
    </div>
    </base-card>
  </li>
</template>

<script>
export default {
  props: ["id", "title", "ingredients", "instructions"],
  inject: ['deleteRecipe'],
};
</script>

<style scoped>
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
div {
  padding: 1rem;
  max-width: 40rem;
}
</style>
