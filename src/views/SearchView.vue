<script setup lang="ts">
    import { ref, watch } from 'vue';
    import type { Countries } from '@/interfaces/interfaces.ts';
    import axios from 'axios';

    const country = ref('')
    const searchCountry = ref('')
    const imgCountry = ref('')

    watch(country, async () => {
        if (country.value !== '') {
            await axios.get(`https://restcountries.com/v3.1/name/${country.value}`)
            .then(response => {
                const data = response.data

                data.forEach((country: Countries) => {
                    searchCountry.value = country.name.common
                    imgCountry.value = country.flags.png
                })
            })
            .catch((error) => {
                console.log('Error ao consumir API: ', error)
            })
        }
    })

</script>

<template>
    
</template>

<style scoped>
</style>
