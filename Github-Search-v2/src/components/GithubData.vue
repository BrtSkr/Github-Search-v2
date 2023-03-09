<template>
    <div>
        <input type="text" v-model="inputValue">
        <button @click="$emit('search', inputValue)">Search</button>
        <h1>{{ apiData }}</h1>
    </div>
</template>
<script setup>
defineProps({
    username: String
})
</script>

<script>
import { defineComponent } from 'vue'
export default defineComponent({
    data() {
        return {
            inputValue: ''
        }
    },
    props: {
    apiData: {
        type: Object,
        default: null
    }
    },
    methods: {
        handleClick() {
            this.$emit('search', this.inputValue)
        }
    }
})
</script>