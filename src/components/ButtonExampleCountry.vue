<script setup lang="ts">
defineProps({
    name: String
})
</script>

<template>
    <v-chip class="text-caption h-0 pa-2 text-md-subtitle-2 pa-md-2" variant="outlined" color="green" :value="name">{{ name }}</v-chip>
</template>

<style scoped>
</style>
