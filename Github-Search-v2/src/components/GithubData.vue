<template>
  <div class="githubData">
    <div class="githubData-input">
        <input type="text" v-model="inputValue" />
        <button @click="$emit('search', inputValue)">Search</button>
    </div>
    <div class="githubData-user" v-if="apiData">
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
  </div>
</template>

<script>
import { defineComponent } from "vue";
import '../SCSS/GithubData.scss';
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
  },
  methods: {
    handleClick() {
      this.$emit("search", this.inputValue);
    },
  },
});
</script>
