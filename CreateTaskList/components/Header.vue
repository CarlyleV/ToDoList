<template>
    <header>
        <h1>{{title}}</h1>
        <Button 
        @task-click="$emit('toggle-add-task')" 
        :text="showAddTask ? '閉じる' : 'タスク追加'" 
        :color="showAddTask ? 'red' : 'green'"
        />
    </header>
</template>

<script>
import Button from './Button.vue'

export default {
    name: 'Header',
    props: {
        title: String,
        showAddTask: Boolean
    },
    components:{
        Button
    }
}
</script>

<style scoped>
    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>