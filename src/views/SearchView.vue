<script setup lang="ts">
    import { ref, watch } from 'vue';
    import type { Countries } from '@/interfaces/interfaces.ts';
    import axios from 'axios';
    import CardCountry from '@/components/CardCountry.vue';
    import ButtonExampleCountry from '@/components/ButtonExampleCountry.vue';

    const searchCountry = ref('') // Recebe o valor informado pelo usuário
    const nameCountry = ref('') // Armazena o nome do país
    const imageCountry = ref('') // Armazena a URL da imagem da bandeira do país
    const capitalCountry = ref('') // Armazena o nome da capital do país
    const populationCountry = ref(0) // Armazena a quantidade da população do país
    const googleMaps = ref('') // Armazena a URL do Google Maps do país
    const area = ref(0) // Armazena a quantidade da área do país
    const independent = ref(false) // Armazena a informação se o país é independente

    // Faz a busca do país informado pelo usuário dentro da API
    watch(searchCountry, async () => {
        if (searchCountry.value !== '') { // Caso searchCountry não seja vazio, executa a requisição
            await axios.get(`https://restcountries.com/v3.1/name/${searchCountry.value}`) // URL da API
            .then(response => { // Caso a requisição seja válida
                const data = response.data // Armazena a resposta da requisição na variável data

                // Percorre a variável (data) para pegar cada dado específico das variáveis
                data.forEach((country: Countries) => {
                    nameCountry.value = country.name.common // Atribui o nome do país a variável reativa (nameCountry)
                    imageCountry.value = country.flags.png // Atribui a URL da imagem da bandeira a variável reativa (imageCountry)
                    capitalCountry.value = country.capital // Atribui o nome da capital a variável reativa (capitalCountry)
                    populationCountry.value = country.population // Atribui a quantidade da população a variável reativa (populationCountry)
                    googleMaps.value = country.maps.googleMaps // Atribui a URL do Google Maps a variável reativa (googleMaps)
                    area.value = country.area // Atribui o valor da área do país a variável reativa (area)
                    independent.value = country.independent // Atribui a resposta se o país é independente a variável reativa (independent)
                })
            })
            .catch((error) => { // Caso a requisição seja inválida
                console.log('Error ao consumir API: ', error) // Retorna uma mensagem no terminal com a especificação do erro
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
