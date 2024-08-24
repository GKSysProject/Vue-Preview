<!-- src/components/SearchSchool.vue -->
<template>
    <div class="search-school">
      <input type="text" v-model="query" @input="search" placeholder="搜索学校..." />
      <ul v-if="suggestions.length">
        <li v-for="suggestion in suggestions" :key="suggestion"><a href="">{{ suggestion }}</a></li>
      </ul>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'SearchSchool',
    data() {
      return {
        query: '',
        suggestions: []
      };
    },
    methods: {
      async search() {
        if (this.query.trim()) {
          try {
            const response = await axios.get(`${this.$config.serverUrl}/search?q=${this.query}`);
            this.suggestions = response.data;
          } catch (error) {
            console.error('Error fetching search suggestions:', error);
          }
        } else {
          this.suggestions = [];
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .search-school {
    position: relative;
    text-align: center;
    width: 40%;
    left: 45%;
    transform: translateX(-50%);
    /* margin-top: 60px; */
  }

input {
  flex: 0 1 50%;
  height: 25px;
  margin-top: 2px;
  padding: 10px 15px;
  border: 1px solid #ccc;
  border-radius: 25px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  font-size: 16px;
  outline: none;
  transition: border-color 0.3s, box-shadow 0.3s, border-radius 0.2;
  width: 100%;
}

input:focus {
  border-color: #007bff;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
  border-radius: 10px;
}
  
ul {
  list-style-type: none;
  padding: 0;
  margin-left: 20px;
}
  
li {
  background: #f4f4f4;
  margin: 5px 0;
  padding: 8px;
  border-radius: 4px;
}
  </style>
  