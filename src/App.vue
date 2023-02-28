
<template>
    <main>
        <header>
            <img src="https://pinia.vuejs.org/logo.svg">
            <h1>Pinia Tasks</h1>
        </header>

        <div class="new-task-form">
            <TaskForm/>
        </div>

        <nav class="filter">
            <button @click="filter='all'">All tasks</button>
            <button @click="filter='favs'">Fav tasks</button>
            <button style="background: #1c03edba; color: white; border: none;" @click="taskStore.$reset" class="reset-store">Reset state</button>
        </nav>

        <div class="loading" v-if="taskStore.loading">
            Loading tasks ...
        </div>

        <div class="task-list" v-if="filter === 'all'">
            <p>All Tasks {{ taskStore.totalCount }}</p>
            <div v-for="task in taskStore.tasks">
                <TaskDetails :task="task"/>
            </div>
        </div>

        <div class="task-list" v-if="filter === 'favs'">
            <p>Fav Tasks {{ taskStore.favCount }}</p>
            <div v-for="task in taskStore.favs">
                <TaskDetails :task="task"/>
            </div>
        </div>

        
    </main>
 
</template>

<script>
    import { useTaskStore } from './stores/TaskStore'
    import TaskDetails from './components/TaskDetails.vue'
    import TaskForm from './components/TaskForm.vue'
    import { ref } from 'vue'
    export default{
        components: {
            TaskDetails,
            TaskForm
        },
        setup() {

            const taskStore = useTaskStore()
            // const { tasks, loading, favs, totalCount, favCount} = storeToRefs(taskStore)

            taskStore.getTasks()

            const filter = ref('all')

            return { taskStore, filter }
        }
    }
</script>

<style scoped>

</style>
