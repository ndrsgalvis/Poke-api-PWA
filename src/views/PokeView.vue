<script setup>
import { useGetData } from '@/composables/getData'
import { useRoute, useRouter } from 'vue-router';
import { useFavoritoStore } from "@/store/favoritos";

    const route = useRoute()
    const router = useRouter()
    const useFavorito = useFavoritoStore()

    const { add, findPoke } = useFavorito
    const {data, getData, loading, error} = useGetData()
    
    const back = () => {
        router.push('/pokemons')
    }

    getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`)
</script>
<template  >
    <p v-if="loading"> Cargando información... </p>
    <div class="alert alert-danger mt-3" v-if="error"> No existe este pokemon </div>
    <div v-if="data" class="text-center">
        <img :src="data.sprites?.front_default" >
        <h1>Pokemon {{$route.params.name}} </h1>
        <button @click="back" class="btn btn-outline-primary me-2">volver</button>
        <button @click="add(data)" :disabled="findPoke(data.name)" class="btn btn-primary">Agregar a favoritos</button>
    </div>
    <div v-else>
        <button @click="back" class="btn btn-outline-primary">volver</button>
    </div>
</template>