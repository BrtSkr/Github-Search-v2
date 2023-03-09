<template>
  <div>
    <GithubData @search="handleSearch" :api-data="apiData"/>
  </div>
</template>

<script>
import { defineComponent } from 'vue'
import GithubData from './components/GithubData.vue';
import axios from 'axios'

export default defineComponent({
  components: { GithubData },
  data() {
  return {
    apiData: null
  }
  },
  methods: {
    async handleSearch(value) {
      try {
        const response = await axios.get(`https://api.github.com/users/${value}`)
        console.log(response.data);
        this.apiData = response.data;
      } catch (error) {
        console.error(error);
      }
    }
  }
})
</script>