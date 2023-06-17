<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view />
  <header>
    <h1 class="namamart">Welcome to Dhiki's Mart</h1>
  </header>

  <div class="new-task-form">
    <TaskForm />
  </div>

  <nav class="filter">
    <button @click="filter = 'all'" class="menusemua">Semua</button>
    <button @click="filter = 'favs'" class="menukesukaan">Kesukaan</button>
  </nav>

  <div class="task-list" v-if="filter === 'all'">
    <p>Kamu mempunyai {{ taskStore.tasks.length }} Belanjaan</p>
    <div v-for="task in taskStore.tasks" :key="task.id">
      <TaskDetails :task="task" />
    </div>
  </div>
  <div class="task-list" v-if="filter === 'favs'">
    <p class="wewe">Anda Memiliki Jumlah {{ taskStore.favs.length }} barang kesukaan</p>
    <div v-for="task in taskStore.favs" :key="task.id">
      <TaskDetails :task="task" />
    </div>
  </div>
</template>
<script>
import { ref } from "vue";
import TaskDetails from "./components/TaskDetails.vue";
import TaskForm from "./components/TaskForm.vue";
import { useTaskStore } from "./stores/TaskStore";

export default {
  components: { TaskDetails, TaskForm },
  setup() {
    const taskStore = useTaskStore();
    const filter = ref("all");

    return { taskStore, filter };
  },
};
</script>

<style>
.namamart {
  color: aquamarine;
}
.menusemua {
  border-radius: 5px;
}
.menukesukaan {
  border-radius: 5px;
  font-family: Arial;
  font-style: italic;
}
.task-list p {
  color: aquamarine;
  font-style: italic;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
