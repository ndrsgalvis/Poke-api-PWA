<script setup>
import axios from 'axios'
import { ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';

    const route = useRoute()
    const router = useRouter()

    const poke = ref({})
    const back = () => {
        router.push('/pokemons')
    }

    const getPoke = async() =>{
        try {
            const {data} = await axios.get(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`)
            poke.value = data
        } catch (error) {
            poke.value = null
        }
    }

    getPoke()
</script>
<template >
    <div v-if="poke">
        <button @click="back" class="btn btn-outline-primary">volver</button>
        <img :src="poke.sprites?.front_default" >
        <h1>Pokemon {{$route.params.name}} </h1>
    </div>
    <div v-else>
        <h1> No existe este pokemon</h1>
        <button @click="back" class="btn btn-outline-primary">volver</button>
    </div>
</template>