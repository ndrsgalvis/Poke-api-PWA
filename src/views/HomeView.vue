<script setup>
import { useCounterStore } from "@/store/counter.js";
import { storeToRefs } from "pinia";

const useCounter = useCounterStore()

const { increment } = useCounter
// to use reactive 
const { count, double } = storeToRefs(useCounter)
</script>

<template>
  <main class="text-center m-5">
    <h1>Home counter: {{ count }}</h1>
    <h2>Double: {{ double }} </h2>
    <button class="btn btn-outline-primary" @click="increment"> Increment </button>
  </main>
</template>
