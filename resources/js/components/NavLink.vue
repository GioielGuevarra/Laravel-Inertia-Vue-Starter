<script setup>
defineProps({
    routeName: String,
})
</script>

<template>
    <Link :href="route(routeName)" 
    class="px-3 py-2 rounded-lg"
    :class="{'bg-slate-700' : $page.component === componentName}"
    >
    
    <slot />
    </Link>
</template>