<template>
  <div>
    <GithubData @search="handleSearch" :api-data="apiData"/>
    <RepositoryData :repository-data="repoData" :userData="apiData"/>
  </div>
</template>

<script>
import { defineComponent } from 'vue'
import GithubData from './components/GithubData.vue';
import RepositoryData from './components/RepositoryData.vue';
import axios from 'axios'

export default defineComponent({
  components: { GithubData, RepositoryData },
  data() {
  return {
    apiData: null,
    repoData: null
  }
  },
  methods: {
    async handleSearch(value) {
      try {
        const response = await axios.get(`https://api.github.com/users/${value}`);
        const repoResponse = await axios.get(`https://api.github.com/users/${value}/repos`);
        this.apiData = response.data;
        this.repoData = repoResponse.data;
        console.log(response.data, 'Response data in App component');
        console.log(repoResponse, 'repoResponse data in App component')
      } catch (error) {
        console.error(error);
      }
    }
  }
})
</script>