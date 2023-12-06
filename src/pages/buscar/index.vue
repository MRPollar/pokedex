<template>
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
                <h1 class="text-5xl font-bold mb-4">Resultado:</h1>
                <div class="grid grid-cols-2 gap-2">
                    <template v-if="pending">
                        <p>carregando</p>
                    </template>
                    <template v-else-if="error">
                        <p>Nada encontrado</p>
                    </template>
                    <template v-else>
                        <CardPokemon :pokemon="data.species"/>
                    </template>
                </div>
            </div>
        </section>
    </div>
</template>

<script setup>
const query = ref();
watchEffect(() => {
    let route = useRoute();
    query.value = route.query.q;
})


const { data, error, refresh, pending } = await useAsyncData(`pokemon:${query.value}`, () => {
        const response = $fetch(`https://pokeapi.co/api/v2/pokemon/${query.value}`);
        return response;
    },
    {
        watch:[query]
    }
)
</script>