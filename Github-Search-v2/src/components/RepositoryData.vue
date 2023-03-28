<template>
  <div v-if="userData" class="repository-top">
    <h1>Repositories: {{ userData.public_repos }}</h1>
    <select v-model="sort" @change="$emit('sort',sort)" name="" id="">
      <option value="default">Default</option>
      <option value="name">Name</option>
      <option value="updated">Last update</option>
      <option value="created">Creation date</option>
    </select>
    <select v-model="direction" @change="$emit('direction',direction)" name="" id="">
      <option value="asc">Ascending</option>
      <option value="desc">Descending</option>
    </select>
  </div>
  <section class="container-repository">
    <div class="repository" v-for="repo in repositoryData" :key="repo.id">
      <p>Name: {{ repo.name }}</p>
      <p>ID: {{ repo.id }}</p>
      <p>Language: {{ repo.language }}</p>
      <p>Created at: {{ repo.created_at.slice(0, 10) }}</p>
      <p>Last update: {{ repo.updated_at.slice(0, 10) }}</p>
      <a :href="repo.html_url" target="_blank">Check</a>
    </div>
  </section>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      sort: "",
      direction: '',
    };
  },
  props: {
    repositoryData: {
      type: Array,
      default: [],
    },
    userData: {
      type: Object,
      default: null,
    },
  },

  methods: {
    handleEmit(){
       
    }
  },
});
</script>
