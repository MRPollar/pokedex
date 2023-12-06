<template>
    <Head>
        <Title>Pokedex</Title>
        <Meta property="og:title" content="Pokedex"/>
        <Meta name="twitter:title" content="Pokedex"/>
        <Meta name="description" content="Conheça o poder dos seus pokemons favoritos"/>
        <Meta property="og:description" content="Conheça o poder dos seus pokemons favoritos"/>
        <Meta name="twitter:description" content="Conheça o poder dos seus pokemons favoritos"/>
        <Meta property="og:url" content="https://meuSite.com"/>
        <Meta property="og:image" content="/imgs/pokedex.jpg"/>
        <Meta name="twitter:image" content="/imgs/pokedex.jpg"/>
        <Meta name="twitter:card" content="summary"/>
    </Head>
    <div>
        <section class="py-5 mb-5">
            <div class="container mx-auto px-2">
                <ClientOnly>
                    <SearchPokemon/>
                </ClientOnly>
            </div>
        </section>
        <section class="py-5">
            <div class="container max-w-4xl mx-auto px-2 font-mono">
                <h1 class="text-5xl font-bold mb-4">Pokemons</h1>
                <div class="grid grid-cols-2 gap-2">
                    <template v-for="pokemon of pokemons.results" :key="pokemon.name">
                        <CardPokemon :pokemon="pokemon"/>
                    </template>
                </div>
            </div>
        </section>
        <!-- <section class="py-5">
            <div class="container max-w-4xl mx-auto px-2 font-mono">
                <ClientOnly>
                    <NavPage :page="page.query.page" :totalPages="totalPages" @pagination-event="pagination($event)"/>
                </ClientOnly>
            </div>
        </section> -->
    </div>
</template>

<script setup>
const page = useRoute();
const itensPorPágina = 20;
const { data:pokemons } = await useAsyncData(
    'pokemons',
    () => {
        let indexStart = page.query?.page != undefined ? (page.query.page - 1) * itensPorPágina : 0;
        const response = $fetch(`https://pokeapi.co/api/v2/pokemon?limit=20&offset=${indexStart}`);
        return response;
    },{watch:[page]}
)

const totalPages = Math.floor(pokemons.value.count)

</script>