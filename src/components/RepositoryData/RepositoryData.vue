<template>
  <div v-if="userData" class="repository-top">
    <h1>Repositories: {{ userData.public_repos }}</h1>
    <select v-model="sort" @change="$emit('sort', sort)" name="" id="">
      <option value="name">Name</option>
      <option value="updated">Last update</option>
      <option value="created">Creation date</option>
    </select>
    <select
      v-model="direction"
      @change="$emit('direction', direction)"
      name=""
      id=""
    >
      <option value="desc">Descending</option>
      <option value="asc">Ascending</option>
    </select>
  </div>
  <section class="container-repository">
    <div class="repository" v-for="repo in repositoryData" :key="repo.id">
      <p class="repository-name">Name: {{ repo.name }}</p>
      <p>
        Language: <span>{{ repo.language }}</span>
      </p>
      <p class="repository-muted">
        Created at: {{ repo.created_at.slice(0, 10) }}
      </p>
      <p class="repository-muted">
        Last update: {{ repo.updated_at.slice(0, 10) }}
      </p>
      <p class="repository-muted">ID: {{ repo.id }}</p>
      <a :href="repo.html_url" target="_blank">Check</a>
    </div>
  </section>
</template>

<script>
import { defineComponent } from "vue";
import './RepositoryData.scss';
export default defineComponent({
  emits: ["sort", "direction"],
  data() {
    return {
      sort: "name",
      direction: "asc",
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
    addColors(item) {
      if (item === "HTML") {
        return "html";
      }
      if (item === "JavaScript") {
        return "javascript";
      }
      if (item === "Vue") {
        return "vue";
      }
      if (item === "SCSS" || item === "SASS") {
        return "sass";
      }
      if (item === "CSS") {
        return "css";
      }
      if (item === "Python") {
        return "python";
      }
      if (item === "C#") {
        return "csharp";
      }
      if (item === "TypeScript") {
        return "typescript";
      }
      if (item === "Kotlin") {
        return "kotlin";
      }
      if (item === "C") {
        return "c";
      }
      if (item === "C++") {
        return "cpp";
      }
      if (item === "Rust") {
        return "rust";
      }
    },
  },
});
</script>
