<script setup lang="ts">
defineProps({
    nameCountry: String,
    capital: String,
    image: String,
    population: Number,
    googleMaps: String,
    area: Number,
    independent: String
})
</script>

<template>
    <v-sheet
        class="text-body-2 mx-auto w-75 border-md"
    >
        <v-container fluid>
            <v-row>
                <v-col cols="12" md="3">
                    <v-img :src="image" cover></v-img>
                </v-col>
                <v-col cols="12" md="9">
                    <h1 class="mb-4">{{ nameCountry }}</h1>
                    <ul class="ps-4 mb-6">
                        <li>Capital: {{ capital }}</li>
                        <li>Area: {{ area }}</li>
                        <li>Population: {{ population }}</li>
                        <li>Independent: {{ independent ? 'Yes' : 'No' }}</li>
                    </ul>
                    <v-btn
                        class="text-none font-weight-bold"
                        color="primary"
                        rounded="0"
                        variant="flat"
                        block
                        :href="googleMaps"
                        target="_blank"
                    >
                        Google Maps
                    </v-btn>
                </v-col>
            </v-row>
        </v-container>
    </v-sheet>
</template>

<style scoped>
li {
    font-size: 16px;
}
</style>
