<template>
    <div class="flex items-center justify-center">
        <form @submit.prevent="buscarPokemon" class="form flex flex-col space-y-6 items-center justify-center">
            <div>
                <input type="text" placeholder="Procurar pokemon..." v-model="search"/>
                <Icon class="icon-search" name="line-md:search-twotone"/>
            </div>
            <button class="px-3 py-2 bg-slate-200 dark:bg-slate-800 rounded-md" type="submit">Pesquisar</button>
        </form>
    </div>
</template>

<script setup>
const search = ref('');

async function buscarPokemon(){
    await navigateTo({ path: '/buscar', query:{ q: search.value.toLowerCase() } })
}
</script>

<style scoped>
.form{
    width: 100%;
    max-width: 500px;
}

.form > div {
    width: 100%;
    position: relative;
}

.form > div .icon-search{
    position: absolute;
    transform: translateY(-50%);
    top: 50%;
    right: 5px
}

.form > div .icon-search{
    @apply text-2xl
}

.form input{
    @apply pr-10 p-2 bg-slate-200 dark:bg-slate-800 rounded-md
}
.form input{
    outline: none;
    width: 100%;
}
</style>