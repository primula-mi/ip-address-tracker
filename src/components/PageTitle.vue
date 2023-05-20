<script setup>
const props = defineProps(["text"]);
</script>
<template>
    <h1 class="title">{{ props.text }}</h1>
</template>
<style scoped>
    .title {
        font-size: var(--font-size-title);
        font-weight: var(--font-weight-normal);
        color: var(--color-white);
    }
</style>