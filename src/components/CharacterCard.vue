<template>
  <div class="character-card">
    <img :src="character.image" alt="Character Image" />
    <h3>{{ character.name }}</h3>
    <p>Status: {{ character.status }}</p>
    <p>Species: {{ character.species }}</p>
  </div>
</template>

<script>
export default {
  props: {
    character: Object
  }
}
</script>

<style scoped>
.character-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 16px;
  text-align: center;
  background-color: #f9f9f9;
}

.character-card img {
  border-radius: 50%;
  width: 150px;
  height: 150px;
}

.character-card h3 {
  margin: 16px 0 8px;
}

.character-card p {
  margin: 4px 0;
}
</style>
