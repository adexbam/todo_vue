<template>
  <div class='container'>
    <h1>My Todo List</h1>
    <input v-model="currentTodo" @keydown.enter="addTodo(todo)" placeholder="Add a todo">
    <ul class="todos">
      <li v-for='(todo, index) in todos' :key='todo.id'>
        <input type='checkbox' v-model='todo.completed' >
          <div> 
          <span 
            class="todo-item-label"
            :class='{completed: todo.completed}' 
            @dblclick='editTodo(todo)' 
            v-if="!todo.edit">
              {{todo.label}}
          </span> 

            <input v-else class="todo-item-edit" type="text" v-model='todo.label' @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)" @keyup.escape="doneEdit(todo)"> 
          </div>
        <button class='closeButton' @click="removeTodo(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: '',
      editedTodo: null
    };
  },
  methods: {
    addTodo() {
      this.todos.push({id: this.todos.length, label: this.currentTodo, completed: false, edit: false});
      this.currentTodo = '';
    },
    removeTodo(index) {
      //var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
     todo.edit = true
    },
    doneEdit(todo) {
     todo.edit = false
    }
  }
};
</script>

<style>
</style>