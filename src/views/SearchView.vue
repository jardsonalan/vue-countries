<script setup lang="ts">
    import { ref, watch } from 'vue';
    import type { Countries } from '@/interfaces/interfaces.ts';
    import axios from 'axios';
    import CardCountry from '@/components/CardCountry.vue';
    import ButtonExampleCountry from '@/components/ButtonExampleCountry.vue';

    const searchCountry = ref('')
    const nameCountry = ref('')
    const imageCountry = ref('')
    const capitalCountry = ref('')
    const populationCountry = ref(0)
    const googleMaps = ref('')
    const area = ref(0)
    const independent = ref('')

    watch(searchCountry, async () => {
        if (searchCountry.value !== '') {
            await axios.get(`https://restcountries.com/v3.1/name/${searchCountry.value}`)
            .then(response => {
                const data = response.data

                data.forEach((country: Countries) => {
                    nameCountry.value = country.name.common
                    imageCountry.value = country.flags.png
                    capitalCountry.value = country.capital
                    populationCountry.value = country.population
                    googleMaps.value = country.maps.googleMaps
                    area.value = country.area
                    independent.value = country.independent
                })
            })
            .catch((error) => {
                console.log('Error ao consumir API: ', error)
            })
        }
    })

</script>

<template>
    <v-container>
        <v-row>
            <v-col>
                <v-img
                    src="logo.png"
                    max-width="200"
                    class="mx-auto"
                />
            </v-col>
        </v-row>
        <v-row class="mt-4">
            <v-col>
                <v-text-field 
                    class="w-75 mx-auto" append-inner-icon="mdi-magnify"
                    clearable
                    v-model="searchCountry"
                    label="Search your country"
                    variant="outlined"
                />
                <div class="d-flex align-center justify-center mt-n5">
                    <p class="text-caption text-md-subtitle-1">Example:</p>
                    <v-chip-group class="ml-2">
                        <ButtonExampleCountry name="Brazil" @click="() => {searchCountry = 'Brazil'}"/>
                        <ButtonExampleCountry name="Germany" @click="() => {searchCountry = 'Germany'}"/>
                        <ButtonExampleCountry name="France" @click="() => {searchCountry = 'France'}"/>
                    </v-chip-group>
                </div>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
                <CardCountry
                    v-if="searchCountry !== ''"
                    :name-country="nameCountry"
                    :capital="capitalCountry[0]"
                    :image="imageCountry"
                    :population="populationCountry"
                    :google-maps="googleMaps"
                    :area="area"
                    :independent="independent"
                />
            </v-col>
        </v-row>
    </v-container>
</template>

<style scoped>
</style>
