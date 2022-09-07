<script setup>
import { useFavoritoStore } from "@/store/favoritos";
import { storeToRefs } from "pinia";
import { RouterLink } from "vue-router";

const useFavorito = useFavoritoStore()
// storeToRefs propiedades reacitvs only NOT METHODS
const { favoritos } = storeToRefs(useFavorito)
// for methods use 
const { remove } = useFavorito

</script>
<template>
    <h2 v-if="favoritos.length == 0" class="text-center m-5"> Sin favoritos </h2>
    <div class="m-4" v-else>
        <h1 class="text-center">Favoritos</h1>
        <ul class="list-group">
            <li class="list-group-item"
                v-for="poke in favoritos"
                :key="poke.id"
            > 
            <div>{{poke.name}}</div>
            <div class="btn btn-danger me-2" @click="remove(poke.id)">Eliminar</div>
            <router-link class="btn btn-outline-primary" :to="`/pokemons/${poke.name}`"> Más info</router-link>
            </li>
        </ul>
    </div>
</template>