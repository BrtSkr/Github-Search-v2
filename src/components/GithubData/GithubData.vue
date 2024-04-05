<template>
  <div class="container-githubData">
    <form @submit.prevent class="githubData-input">
      <input placeholder="Username" type="text" v-model="inputValue" />
      <button type="submit" @click="$emit('search', inputValue)">Search</button>
    </form>
    <div class="githubData" v-if="apiData">
      <div class="githubData-user">
        <img :src="apiData.avatar_url" alt="User avatar" />
        <div class="githubData--user-block">
          <a :href="apiData.html_url">Nickname: {{ apiData.login }}</a>
          <p>Name: {{ apiData.name }}</p>
          <p v-if="apiData.email">Email: {{ apiData.email }}</p>
          <p>ID: {{ apiData.id }}</p>
          <p>Created at: {{ apiData.created_at.slice(0, 10) }}</p>
          <p>Followers: {{ apiData.followers }}</p>
          <p>Location: {{ apiData.location }}</p>
        </div>
      </div>

      <section v-if="starredData" class="githubData--starred-container">
        <h2>Starred</h2>
        <div v-for="starred in starredData" class="githubData-starred">
          <p>{{ starred.owner.login }}</p>
          <a :href="starred.html_url">{{ starred.name }}</a>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import "./GithubData.scss";
export default defineComponent({
  data() {
    return {
      inputValue: "",
    };
  },
  props: {
    apiData: {
      type: Object,
      default: null,
    },
    starredData: {
      type: Array,
      default: null,
    },
  },
  methods: {
    handleClick() {
      this.$emit("search", this.inputValue);
    },
  },
});
</script>
