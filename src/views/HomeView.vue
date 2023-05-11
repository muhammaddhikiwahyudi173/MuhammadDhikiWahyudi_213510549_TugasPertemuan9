<template>
  <h1 class="judulbesar">
    Selamat Datang Di Website TODO List by Muhammad Dhiki Wahyudi
  </h1>
  <div>
    <input v-model="newTodo" placeholder="Masukkan Kegiatan" />
    <button @click="addTodo" class="tombol">Tambah Kegiatan</button>
    <br /><br />
    <button @click="hideCompleted = !hideCompleted" class="tmbhps">
      {{ hideCompleted ? "Tampilkan Semua" : "Sembunyikan yang sudah selesai" }}
    </button>
    <ul>
      <li v-for="todo in visibleTodos" :key="todo.id">
        <span
          :class="{ completed: todo.completed }"
          @click="toggleComplete(todo)"
          class="isi">{{ todo.text }}</span
        >
        <button
          v-if="!todo.completed"
          @click="completeTodo(todo.id)"
          class="tmblsls"
        >
          Selesai
        </button>
        <button
          v-if="todo.completed"
          @click="unCompleteTodo(todo.id)"
          class="tmblslsi"
        >
          Belum Selesai
        </button>
        <button @click="removeTodo(todo.id)" class="tmblhps">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      todos: [],
      newTodo: "",
      nextId: 1,
      hideCompleted: false,
    };
  },
  computed: {
    visibleTodos() {
      if (this.hideCompleted) {
        return this.todos.filter((todo) => !todo.completed);
      } else {
        return this.todos;
      }
    },
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== "") {
        this.todos.push({
          id: this.nextId++,
          text: this.newTodo,
          completed: false,
        });
        this.newTodo = "";
      }
    },
    removeTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    completeTodo(id) {
      const todo = this.todos.find((todo) => todo.id === id);
      if (todo) {
        todo.completed = true;
      }
    },
    unCompleteTodo(id) {
      const todo = this.todos.find((todo) => todo.id === id);
      if (todo) {
        todo.completed = false;
      }
    },
    toggleComplete(todo) {
      todo.completed = !todo.completed;
    },
  },
};
</script>

<style>
ul {
  list-style: none;
  padding: 0;
}
li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
.completed {
  text-decoration: line-through;
}
button {
  margin-left: 10px;
}
body {
  background-color: brown;
  font-family: sans-serif;
  text-decoration: underline;
}
.judulbesar {
  color: blanchedalmond;
  font-style: italic;
  font-family: Cambria;
}
.tombol {
  border-radius: 8px;
  font-style: italic;
  font-family: Cambria;
  border-color: aquamarine;
  border-width: 4px;
  font-style: italic;
  color: black;
  font-weight: bold;
}
.tmblsls {
  border-radius: 6px;
  border-color: green;
  border-width: 7px;
  font-style: italic;
  font-weight: bold;
  color: black;
  font-family: calibri;
}
.tmblslsi {
  border-radius: 6px;
  border-color: yellow;
  border-width: 7px;
  font-style: italic;
  font-weight: bold;
  color: black;
  font-family: calibri;
}
.tmblhps {
  border-radius: 6px;
  border-color: blue;
  border-width: 7px;
  font-style: italic;
  font-weight: bold;
  color: red;
  font-family: calibri;
}
.isi{
  color: white;
  font-weight: bold;
  font-family: calibri;
  font-style: italic;
}
.tmbhps{
  border-radius: 6px;
  border-color: purple;
  border-width: 7px;
  font-style: italic;
  font-weight: bold;
  color: red;
  font-family: calibri;
}
</style>
