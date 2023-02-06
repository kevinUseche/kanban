<script setup>

    import { reactive, ref } from 'vue';
    import Column from './Column.vue';

    const columns = reactive([])

    const nameColumn = ref('')

    function handleCreateColumn(){
        if (nameColumn.value !== ''){
            columns.push({
                id: crypto.randomUUID(),
                title: nameColumn.value,
                elements: []
            })
            nameColumn.value = ''
            return
        }
        alert('Añadir nombre de la columna')
    }

    function handleCreateElement(value, column){
        column.elements.push({
            id: crypto.randomUUID(),
            title: value
        })
    }

    function handleStartDrag(event, column, element){
        event.dataTransfer.setData(
            'text/plaint',
            JSON.stringify({ columnId: column.id, elementId: element.id})
        )
    }

    function onDrop(event, column){
        const { columnId, elementId } = JSON.parse(event.dataTransfer.getData('text/plaint'))
        const columnOrigin = columns.find(_column => _column.id === columnId)
        const elementOrigin = columnOrigin.elements.find(_element => _element.id === elementId)
        column.elements.push(elementOrigin)
        columnOrigin.elements = columnOrigin.elements.filter(_element => _element.id !== elementOrigin.id)
    }

</script>

<template>
    <div class="content-board">
        <Column 
            v-for="(column, index) in columns" 
            :key="index" 
            :column="column"
            @drop="onDrop($event, column)"
            @dragover.prevent
            @dragenter.prevent
            @on-start-drag="({event, element}) => handleStartDrag(event, column, element)"
            @on-new-element="value => handleCreateElement(value, column)"
        />
        <div class="form-new-column">
            <div class="content-form">
                <input 
                    type="text" 
                    placeholder="Titulo de la columna"
                    v-model="nameColumn"
                >
                <button 
                    class="btn-add"
                    @click="handleCreateColumn"
                >
                    Añadir columna
                </button>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .content-board{
        display: grid;
        gap: 2rem;
        grid-template-columns: repeat(auto-fill, minmax(20rem, 1fr));
        padding: 2rem 0;
    }
    .content-form{
        background-color: var(--ligth-green);
        padding: 2rem;
    }
    .content-form input{
        padding: 1rem 0;
        border: none;
        margin-bottom: 1rem;
    }
    .btn-add{
        display: block;
        padding: 1rem;
        border: none;
        background-color: var(--red);
        color: var(--white);
        text-transform: capitalize;
        cursor: pointer;
    }
</style>