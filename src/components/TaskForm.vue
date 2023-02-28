<template>
    <form @submit.prevent="handleSubmit">
        <input 
            type="text"
            placeholder="I need to ..."
            v-model="newTask"
        >

        <button>Add</button>

    </form>
</template>


<script setup>
    import { useTaskStore } from '../stores/TaskStore'
    import { ref } from 'vue'

    const taskStore = useTaskStore()
    const newTask = ref('')

    function handleSubmit() {
        if(newTask.value.length > 0){
            taskStore.addTask({
                title: newTask.value,
                isFav: false,
                id: Math.floor(Math.random() * 100000)
            })
            newTask.value = ''
        }
    }

</script>