<script setup>
    import { toRefs, ref, defineEmits } from 'vue'
    import Element from './Element.vue'

    const props = defineProps({
        column: Object
    })
    const { column } = toRefs(props)

    const nameElement = ref('')
    const emits = defineEmits(['onNewElement', 'onStartDrag'])

    function handleSubmit(){
        if(nameElement.value !== ''){
            emits("onNewElement", nameElement.value)
            nameElement.value = ''
            return
        }
        alert('Añadir un nombre al elemento')
    }

    function startDrag(event, element){
        emits("onStartDrag", {event, element})
    }
</script>

<template>
    <div class="column">
        <h3 class="title-column">{{ column.title }}</h3>
        <div class="column-elements">
            <Element 
                v-for="(element, index) in column.elements" 
                :key="index"
                :element="element"
                draggable="true"
                @dragstart="event => startDrag(event, element)"
            />
            <div class="form-new-element">
                <form action="" @submit.prevent="handleSubmit">
                    <input 
                        type="text" 
                        placeholder="Nuevo elemento"
                        v-model="nameElement"
                    >
                </form>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .column{
        background-color: var(--ligth-green);
        padding: 2rem;
    }
    .title-column{
        color: var(--white);
    }
    .form-new-element form input{
        display: block;
        width: 100%;
        padding: 2rem;
    }
</style>