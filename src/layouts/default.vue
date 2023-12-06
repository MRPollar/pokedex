<template>
    <div>
        <header class="py-4 bg-slate-200 dark:bg-slate-800">
            <div class="container mx-auto">
                <nav class="px-2 flex items-center justify-between">
                    <NuxtLink to="/">
                        <img src="/imgs/logo-pokedex.png" width="120"/>
                    </NuxtLink>
                    <ClientOnly>
                        <ColorMode/>
                    </ClientOnly>
                </nav>
            </div>
        </header>
        <main>
            <slot/>
        </main>
    </div>
</template>