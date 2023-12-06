<template>
    <nav class="flex items-center justify-center">
        <ul class="pagination-list flex items-center bg-slate-200 dark:bg-slate-800">
            <template v-if="page > 1">
                <NuxtLink class="pagination hover:bg-stone-500 duration-200"><Icon name="bxs:up-arrow" style="rotate: 270deg"/></NuxtLink>
                <NuxtLink class="pagination hover:bg-stone-500 duration-200" v-if="page > 2">{{ page - 2 }}</NuxtLink>
                <NuxtLink class="pagination hover:bg-stone-500 duration-200">{{ page - 1 }}</NuxtLink>
            </template>
            <NuxtLink class="pagination bg-stone-400 hover:bg-stone-500 duration-200">{{ page + 1 }}</NuxtLink>
            <template v-if="page < totalPages">
                <NuxtLink :to="`/?page=${ page+1 }`" class="pagination hover:bg-stone-500 duration-200">{{ page + 2 }}</NuxtLink>
                <NuxtLink class="pagination hover:bg-stone-500 duration-200" v-if="page < totalPages - 1">{{ page + 3 }}</NuxtLink>
                <NuxtLink class="pagination hover:bg-stone-500 duration-200"><Icon name="bxs:up-arrow" style="rotate: 90deg"/></NuxtLink>
            </template>
        </ul>
    </nav>
</template>

<script setup>
defineProps({
    page:{
        type: Number,
        default: 1
    },
    totalPages:Number
})
</script>

<style scoped>
.pagination-list{
    border-radius: 4px;
    overflow: hidden;
}
.pagination{
    width: 40px;
    height: 40px;
    cursor: pointer;
}

.pagination{
    @apply flex items-center justify-center
}
</style>