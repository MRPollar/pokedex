<template>
    <NuxtLink :to="`pokemon/${pokemon.name}`" class="card-pokemon">
        <div class="mb-3">
            <h2 class="p-2 text-3xl flex items-center gap-2">
                <ClientOnly>
                    <Icon name="ic:twotone-catching-pokemon"/>
                </ClientOnly>{{pokemon.name}}
            </h2>
        </div>
        <div class="my-img rounded-md">
            <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/${img}.png`" />
            <ClientOnly>
                <Icon class="bg-img" name="ic:twotone-catching-pokemon"/>
            </ClientOnly>
        </div>
    </NuxtLink>
</template>

<script setup>
const props = defineProps({
    pokemon:Object
})
const img = computed(() => {
    let urlArray = props.pokemon.url.split('/');
    return urlArray[urlArray.length - 2];
})
</script>

<style scoped>
.card-pokemon{
    @apply bg-red-700 rounded-md bg-slate-200 dark:bg-slate-800
}
.card-pokemon{
    display: flex;
}

.card-pokemon > .my-img{
    /* background-color: red; */
    overflow: hidden;
    position: relative;
}

.card-pokemon > .my-img > img{
    z-index: 2;
    position: relative;
    max-width: 100%;
}

.card-pokemon > .my-img > .bg-img{
    position: absolute;
    top: 80%;
    left: 80%;
    font-size: 300px;
    transform: translate(-50%,-50%) rotate(-45deg);
    z-index: 1;
    opacity: .5;
}

@media screen and (max-width: 768px) {
    .card-pokemon{
        position: relative;
        flex-direction: column;
        align-items: center;
        justify-content:end;
        min-height: 335px;
    }
    .card-pokemon > .my-img{
        position: relative;
    }
    .card-pokemon > .my-img > .bg-img{
        font-size: 500px;
    }
}
</style>