<template>
  <div>
    <GithubData
      @search="handleValue"
      :api-data="searchState.apiData"
      :starred-data="searchState.starredData"
    />
    <RepositoryData
      @sort="handleSort"
      @direction="handleDirection"
      :repository-data="searchState.repoData"
      :userData="searchState.apiData"
    />
  </div>
</template>

<script>
import { defineComponent, reactive } from "vue";
import GithubData from "./components/GithubData.vue";
import RepositoryData from "./components/RepositoryData.vue";
import axios from "axios";

export default defineComponent({
  components: { GithubData, RepositoryData },
  setup() {
    const searchState = reactive({
      apiData: null,
      repoData: null,
      starredData: null,
      value: "",
      sort: "",
      direction: "desc",
    });
    const handleSearch = async () => {
      try {
        const response = await axios.get(
          `https://api.github.com/users/${searchState.value}`
        );
        const repoResponse = await axios.get(
          `https://api.github.com/users/${searchState.value}/repos?sort=${searchState.sort}&direction=${searchState.direction}`
        );
        const starredResponse = await axios.get(
          `https://api.github.com/users/${searchState.value}/starred`
        );
        searchState.apiData = response.data;
        searchState.repoData = repoResponse.data;
        searchState.starredData = starredResponse.data;
        console.log(response.data, "Response data in App component");
        console.log(repoResponse.data, "repoResponse data in App component");
        console.log(starredResponse.data, "starredResponse in App component");
      } catch (error) {
        console.error(error);
      }
    };
    const handleSort = (sort) => {
      searchState.sort = sort;
      handleSearch(searchState.value);
    };
    const handleDirection = (direction) => {
      searchState.direction = direction;
      handleSearch(searchState.value);
    };
    const handleValue = (value) => {
      searchState.value = value;
      handleSearch(searchState.value);
    };
    return {
      searchState,
      handleSearch,
      handleDirection,
      handleSort,
      handleValue,
    };
  },
});
</script>
