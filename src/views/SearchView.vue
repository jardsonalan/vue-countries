<script setup lang="ts">
    import { ref, watch } from 'vue';
    import type { Countries } from '@/interfaces/interfaces.ts';
    import axios from 'axios';
    import CardCountry from '@/components/CardCountry.vue';

    const searchCountry = ref('')
    const nameCountry = ref('')
    const imageCountry = ref('')
    const capitalCountry = ref('')
    const populationCountry = ref(0)

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
                <v-text-field class="w-75 mx-auto" append-inner-icon="mdi-magnify" clearable v-model="searchCountry" label="Search your country" variant="outlined"/>
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
                />
            </v-col>
        </v-row>
    </v-container>
</template>

<style scoped>
</style>
