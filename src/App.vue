<template>
  <div id="app">
    <h1>Todo List</h1>
    <input class="todo-input" v-model="newTodo"  @keyup.enter="addTodo" placeholder="Add a new todo" />
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <TodoItem :todo="todo" @update="updateTodo" @remove="removeTodo(index)" />
      </li>
    </ul>
  </div>
</template>

<script>
import TodoItem from './components/TodoItem.vue';

export default {
  name: 'App',
  components: {
    TodoItem
  },
  data() {
    return {
      newTodo: '',
      todos: []
    };
  },
  created() {
    this.loadTodos();
  },
  methods: {
    loadTodos() {
      const todos = localStorage.getItem('todos');
      if (todos) {
        this.todos = JSON.parse(todos);
      }
    },
    saveTodos() {
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
    addTodo() {
      if (this.newTodo.trim()) {
        this.todos.push({ text: this.newTodo.trim(), completed: false });
        this.newTodo = '';
        this.saveTodos();
      }
    },
    updateTodo() {
      this.saveTodos();
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
      this.saveTodos();
    }
  }
};
</script>

<style>
body {
  font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
  background: #f5f7fa;
  margin: 0;
  padding: 20px;
  color: #2c3e50;
}

#app {
  max-width: 600px;
  margin: 2rem auto;
  padding: 2rem;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

h1 {
  color: #3498db;
  font-size: 2.5rem;
  margin-bottom: 1.5rem;
  text-align: center;
}

.todo-input {
  width: 100%;
  max-width: 400px;
  padding: 12px 15px;
  border: 1px solid #ddd;
  border-radius: 6px;
  font-size: 16px;
  margin: 10px 0;
  transition: all 0.3s ease;
  outline: none;
}

.todo-input:focus {
  border-color: #4CAF50;
  box-shadow: 0 0 5px rgba(76, 175, 80, 0.2);
}

.todo-input::placeholder {
  color: #999;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 0.8rem;
}
</style>