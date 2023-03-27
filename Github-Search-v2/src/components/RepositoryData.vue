<template>
    <h1 v-if="userData">Repositories: {{ userData.public_repos }}</h1>
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
import { defineComponent } from 'vue';

export default defineComponent({
    props: {
        repositoryData: {
            type: Array,
            default: []
        },
        userData: {
            type: Object,
            default: null
        }
    },
    methods: {

    }
})
</script>