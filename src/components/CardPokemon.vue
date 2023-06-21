<script setup>
import { onBeforeMount, ref } from "vue";

const props = defineProps({
	name: {
		type: String,
		default: null,
	},
	url: {
		type: String,
	},
});

let pokeDetails = ref({});
let pokemonImg = ref();
let pokemonId = ref();
let pokemonType = ref();
let pokeType = ref("");
let pokeAttack = ref();
let pokeDefense = ref();

onBeforeMount(async () => {
	const response = await fetch(props.url);
	const data = await response.json();

	pokeDetails.value = data;
	pokemonImg.value = pokeDetails.value.sprites.other.home.front_default;
	pokemonId.value = pokeDetails.value.id;
	pokemonType.value = pokeDetails.value.types[0].type.name;
	pokeType = pokemonType.value;
	pokeAttack.value = pokeDetails.value.stats[1].base_stat;
	pokeDefense.value = pokeDetails.value.stats[2].base_stat;
});

</script>

<template>
	<div>
		<picture>
			<img :src="pokemonImg" alt="Imagen de Pokemon" />
		</picture>
		<div>
			<h2>
				N.º {{ pokemonId }}
			</h2>
			<h1>
				{{ props.name }}
			</h1>
			<p>
				{{ pokeType }}
			</p>
		
		</div>
		<div>
			<div>
				<p>
					<span>Weight: </span>{{ pokeDetails.weight }}kg
				</p>
				<p>
					<span>Height: </span>{{ pokeDetails.height }}m
				</p>
			</div>
		
		</div>
	</div>
</template>

<style lang="css" scoped></style>
