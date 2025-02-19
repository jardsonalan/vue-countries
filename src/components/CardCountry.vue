<script setup lang="ts">
defineProps({
    nameCountry: String,
    capital: String,
    image: String,
    population: Number
})
</script>

<template>
    <v-card class="w-75 mx-auto">
        <v-img :src="image"></v-img>
        <v-card-title class="font-weight-bold text-center">{{ nameCountry }}</v-card-title>
        <v-card-subtitle class="text-center">{{ capital }}</v-card-subtitle>
        <v-card-text class="text-center">População: {{ population }}</v-card-text>
    </v-card>
</template>

<style scoped>
</style>
