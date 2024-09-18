<template>
  <header>
    <h1>{{ title }}</h1>
  </header>
</template>

<script>
export default {
  props: ["title"],
};
</script>

<!--border-radius and below is customized by me, take away to reset-->
<style scoped>
header {
  width: 100%;
  height: 5rem;
  background-color: #640032;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0.5rem auto;
}

header h1 {
  color: white;
  margin: 0;
}
</style>
