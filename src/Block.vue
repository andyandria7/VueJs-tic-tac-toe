<script setup>
defineProps({
    bloc: String
})

const emit = defineEmits(['click'])
</script>

<template>
    <div @click="emit('click')" >{{ bloc }}</div>
</template>

<style>

</style>