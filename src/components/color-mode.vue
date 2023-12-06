<template>
    <button :title="mode" @click="alterarColor" class="text-2xl p-1 hover:bg-slate-300 hover:dark:bg-slate-900 flex items-center justify-between rounded-md">
        <Icon :name="iconMode[mode]"/>
    </button>
</template>

<script setup>
const useMode = useColorMode();
const iconMode = {
    system:'ph:cloud-moon-duotone',
    dark:'ph:moon-duotone',
    light:'ph:sun-duotone',
};
const modeTheme = [
    'system',
    'dark',
    'light'
]

const mode = computed(() => {
    const indexTheme = modeTheme.indexOf(useMode.preference);
    let newIndex = null;
    if(indexTheme == modeTheme.length - 1)
        newIndex = 0;
    else
        newIndex = indexTheme + 1;

    return modeTheme[newIndex];
})

// const icon = iconMode[mode.value];
const alterarColor = () => useMode.preference = mode.value;
</script>

