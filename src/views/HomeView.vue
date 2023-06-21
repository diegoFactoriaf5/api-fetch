<script setup>
import Pokemon from '@/services/apiPokemon.js';
import { ref, onBeforeMount } from 'vue';
import CardPokemon from '@/components/CardPokemon.vue';

const service = new Pokemon([]); //instanciando mi clase

let pokemons = ref();

onBeforeMount(async () => {
  pokemons.value = await service.fetchAll();
})

</script>

<template>
  <main>
    <div>
      <div>
        <CardPokemon v-for="pokemon in pokemons" :key="pokemon.url" :url="pokemon.url" :name="pokemon.name" />
      </div>
    </div>
  </main>
</template>

<style scoped lang="css"></style>