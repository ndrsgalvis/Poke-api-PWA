<script setup>
import { useGetData } from '../composables/getData';
import { RouterLink } from 'vue-router';

    const {data, getData, loading, error} = useGetData()
    getData('https://pokeapi.co/api/v2/pokemon')

</script>
<template>
    <p v-if="loading">Cargando información</p>
    <div class="alert alert-danger" v-if="error"> {{error}}</div>
    
    <div v-if="data">
      <h1 class="text-center m-3">Pokemons page</h1>
      <ul class="list-group">
        <li class="list-group-item" v-for="pokemon in data.results">
            <router-link :to="`/pokemons/${pokemon.name}`"> {{pokemon.name}} </router-link>
        </li>
      </ul>
      <div class="text-center m-3">
          <button class="btn btn-outline-primary me-3" @click="getData(data.previous)" :disabled="!data.previous"> Preview </button>
          <button class="btn btn-primary" @click="getData(data.next)" :disabled="!data.next"> Next </button>
      </div>

    </div>
</template>
