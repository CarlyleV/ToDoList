<template>
    <div class="container">
      <Header @toggle-add-task="toggleAddTask" 
        title="ToDo" 
        :showAddTask="showAddTask"
        />
    <transition name="fade" appear>
      <div v-if="showAddTask" >
      <AddTask @add-task="addTask"/>
      </div>
      </transition>
      <Tasks  @toggle-reminder="toggleReminder"
              @delete-task="deleteTask" 
      :tasks="tasks" />
       </div>
     
</template>

<script>
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return{
      tasks: [],
      showAddTask: false
    }
  },
  methods: {
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },
    addTask(task){
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id){
      if(confirm('削除しますか')){
      this.tasks = this.tasks.filter((task) => task.id !==id)}
    },
    toggleReminder(id){
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder}:
        task)
    }
  },

  
 
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=M+PLUS+Rounded+1c&family=Open+Sans+Condensed:wght@700&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'M PLUS Rounded 1c', sans-serif;
  font-weight: 900;
  letter-spacing : 1px;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 900px;
  padding: 30px;
  border-radius: 30px;
  background-color: rgb(255, 255, 255);
  box-shadow: 0px 20px 30px -10px rgb(117, 117, 117);
  
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 100px;
  cursor: pointer;
  text-decoration: none;
  font-size: 12px;
  font-family: inherit;
  width: 140px;
  height: 40px;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
