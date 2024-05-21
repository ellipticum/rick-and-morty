<template>
    <div class="home">
      <div class="filters">
        <input type="text" v-model="name" placeholder="Search by name" @input="fetchCharacters" />
        <select v-model="status" @change="fetchCharacters">
          <option value="">All statuses</option>
          <option value="alive">Alive</option>
          <option value="dead">Dead</option>
          <option value="unknown">Unknown</option>
        </select>
      </div>
      <div class="character-list">
        <CharacterCard v-for="character in characters" :key="character.id" :character="character" />
      </div>
      <div class="pagination">
        <button @click="prevPage" :disabled="page === 1">Previous</button>
        <span>Page {{ page }}</span>
        <button @click="nextPage" :disabled="!hasNextPage">Next</button>
      </div>
    </div>
  </template>
  
  <script>
  import api from '../api'
  import CharacterCard from '../components/CharacterCard.vue'
  
  export default {
    name: 'HomeView',
    components: { CharacterCard },
    data() {
      return {
        characters: [],
        page: 1,
        name: '',
        status: '',
        hasNextPage: true
      }
    },
    methods: {
      async fetchCharacters() {
        const response = await api.getCharacters(this.page, this.name, this.status)
        this.characters = response.data.results
        this.hasNextPage = response.data.info.next !== null
      },
      nextPage() {
        if (this.hasNextPage) {
          this.page++
          this.fetchCharacters()
        }
      },
      prevPage() {
        if (this.page > 1) {
          this.page--
          this.fetchCharacters()
        }
      }
    },
    created() {
      this.fetchCharacters()
    }
  }
  </script>
  
  <style scoped>
  .home {
    max-width: 1200px;
    margin: 0 auto;
    padding: 16px;
  }
  
  .filters {
    display: flex;
    justify-content: space-between;
    margin-bottom: 16px;
  }
  
  .filters input, .filters select {
    padding: 8px;
    font-size: 16px;
    width: 48%;
  }
  
  .character-list {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 16px;
  }
  
  .pagination {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 16px;
  }
  
  .pagination button {
    padding: 8px 16px;
    font-size: 16px;
    margin: 0 8px;
  }
  </style>
  