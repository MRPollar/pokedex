<template>
  <Head>
    <Link rel="icon" type="image/png" href="/favicon.png"/>
  </Head>
  <div>
    <NuxtLayout>
      <NuxtPage/>
    </NuxtLayout>
  </div>
</template>

<script setup>
useHead({
  htmlAttrs:{
    lang: 'pt-BR'
  }
})
</script>

<style>
body{
  @apply text-slate-950 dark:text-slate-100 bg-slate-100 dark:bg-slate-950 duration-500
}
</style>
