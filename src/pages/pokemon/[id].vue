<template>
    <Head>
        <Title>Pokedex - {{ pokemon.name }}</Title>
        <Meta property="og:title" :content="`Pokedex - ${pokemon.name}`"/>
        <Meta name="twitter:title" :content="`Pokedex - ${pokemon.name}`"/>
        <Meta name="description" :content="`Atributos do pokemon ${pokemon.name}`"/>
        <Meta property="og:description" :content="`Atributos do pokemon ${pokemon.name}`"/>
        <Meta name="twitter:description" :content="`Atributos do pokemon ${pokemon.name}`"/>
        <Meta property="og:url" content="https://meuSite.com"/>
        <Meta property="og:image" :content="pokemon.sprites.other['official-artwork'].front_default"/>
        <Meta name="twitter:image" :content="pokemon.sprites.other['official-artwork'].front_default"/>
        <Meta name="twitter:card" content="summary"/>
    </Head>
    <section class="py-7">
        <div class="container mx-auto px-2">
            <h1 class="text-5xl font-semibold font-mono mb-6">{{ pokemon.name }}</h1>
            <div class="grid grid-cols-8 gap-4">
                <div class="container-my-img">
                    <img :src="pokemon.sprites.other['official-artwork'].front_default" :alt="pokemon.name"/>
                    <Icon
                        :title="pokemon.types[0].type.name"
                        :name="icons[pokemon.types[0].type.name]"
                        class="type"
                        :class="{
                            'text-red-500':pokemon.types[0].type.name == 'fire',
                            'text-green-400':pokemon.types[0].type.name == 'grass',
                            'text-green-400':pokemon.types[0].type.name == 'bug',
                            'text-cyan-300':pokemon.types[0].type.name == 'water',
                            'text-zinc-400 dark:text-zinc-200':pokemon.types[0].type.name == 'normal',
                            'text-violet-600':pokemon.types[0].type.name == 'poison',
                            'text-yellow-300':pokemon.types[0].type.name == 'electric',
                            'text-lime-500':pokemon.types[0].type.name == 'ground',
                            'text-indigo-300':pokemon.types[0].type.name == 'fairy',
                            'text-rose-500':pokemon.types[0].type.name == 'fighting',
                            'text-yellow-400':pokemon.types[0].type.name == 'psychic',
                            'text-orange-800':pokemon.types[0].type.name == 'rock',
                            'text-purple-600':pokemon.types[0].type.name == 'ghost',
                        }"
                    />
                </div>
                <div class="col-span-5">
                    <ul>
                        <li class="flex items-center justify-between mb-3 border-b-2 p-1" v-for="stat of pokemon.stats">
                            <span class="text-2xl text-slate-400 dark:text-slate-600">{{ stat.stat.name }}</span>
                            <span>{{ stat.base_stat }}</span>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
const route = useRoute();
const { data:pokemon } = await useAsyncData(
    'pokemon',
    () => $fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.id}`)
)
const icons = {
    fire: 'mdi:fire',
    grass: 'game-icons:high-grass',
    bug: 'ant-design:bug-filled',
    water: 'entypo:water',
    normal: 'nonicons:vim-normal-mode-16',
    poison: 'game-icons:poison-gas',
    electric: 'ic:outline-electric-bolt',
    ground: 'game-icons:ground-sprout',
    fairy: 'mdi:fairy',
    fighting: 'mdi:sword-fight',
    psychic: 'game-icons:psychic-waves',
    rock: 'game-icons:rock',
    ghost: 'mingcute:ghost-fill'
}
</script>

<style scoped>
.container-my-img{
    position: relative;
}

.container-my-img > .type{
    position: absolute;
    right: 10px;
    top: 10px;
    font-size: 50px;
}
.container-my-img{
    @apply col-span-3 bg-slate-200 dark:bg-slate-800 flex items-center justify-center rounded-md
}
</style>