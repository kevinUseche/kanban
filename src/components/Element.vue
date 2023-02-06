<script setup>
    const props = defineProps({
        element: Object
    })

    const { element } = props
</script>

<template>
    <div class="element">
        <h4 class="title-element">{{ element.title }}</h4>
    </div>
</template>

<style scoped>
    .element{
        padding: 2rem;
        margin: 1rem 0;
        background-color: var(--orange);
    }
    .title-element{
        color: var(--white);
    }
</style>