<template>
  <div class="todo-container">
    <h1>Todo List</h1>
    <div class="input-wrapper">
      <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add new todo">
      <button @click="addTodo">Add Todo</button>
    </div>
    <ul>
      <li v-for="todo in todos" :key="todo.id" class="todo-item">
        {{ todo.task }}
        <button @click="deleteTodo(todo.id)" class="delete-btn">Delete</button>
      </li>
    </ul>
  </div>
</template>


<script>
import supabase from '../../supabase';

export default {
  data() {
    return {
      todos: [],
      newTodo: ''
    }
  },
  async created() {
    await this.fetchTodos();
  },
  methods: {
    async fetchTodos() {
      let { data: todos, error } = await supabase
        .from('todos')
        .select('*');
      if (error) console.log('error', error);
      else this.todos = todos;
    },
    async addTodo() {
      if (!this.newTodo) return;
      const { error } = await supabase
        .from('todos')
        .insert([
          { task: this.newTodo }
        ]);
      if (error) console.log('error', error);
      else this.fetchTodos();
      this.newTodo = '';
    },
    async deleteTodo(id) {
      const { error } = await supabase
        .from('todos')
        .delete()
        .match({ id });
      if (error) console.log('error', error);
      else this.fetchTodos();
    }
  }
}
</script>

<style scoped>
.todo-container {
  max-width: 600px;
  margin: 30px auto;
  padding: 20px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  border-radius: 8px;
  background-color: #fff;
}

.input-wrapper {
  margin-bottom: 20px;
  display: flex;
  align-items: center;
}

input {
  flex: 1;
  padding: 10px;
  font-size: 16px;
  border: 2px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
}

button {
  padding: 10px 20px;
  background-color: #007BFF;
  border: none;
  color: white;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #0056b3;
}

.todo-item {
  background-color: #f9f9f9;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 4px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.delete-btn {
  background-color: #dc3545;
}

.delete-btn:hover {
  background-color: #c82333;
}
</style>