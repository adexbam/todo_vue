<template>
  <div class='container'>
    <h1>My Todo List</h1>
      <md-card class="cardBox">
      <md-field>
       <md-input v-model="currentTodo" @keydown.enter="addTodo(todo)" placeholder="Click to add a todo"></md-input>
      </md-field>
      <ul class="todos">
        <li v-for='(todo, index) in todos' :key='todo.id'>
          <input class='checkboxButton' type='checkbox' v-model='todo.completed' >
            <span 
              class="todo-item-label"
              :class='{completed: todo.completed}' 
              @dblclick='editTodo(todo)' 
              v-if="!todo.edit">
                {{todo.label}}
            </span> 
            <md-input v-else class="todo-item-edit" type="text" v-model='todo.label' @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)" @keyup.escape="doneEdit(todo)"></md-input> 
          <md-raised class='removeTodoButton' @click="removeTodo(index)">Cancel</md-raised>
        </li>
      </ul>
      </md-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [
        {
          'id': 1,
          'label': 'let us start',
          'completed': true,
          'edit': false
        },
      ],
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
#app {
  font-family: 'Roboto', Helvetica, Arial, sans-serif;
}
li {
  list-style: none;
}
.container {
  width: 50%;
  margin: auto;
  text-align: center;
}

@media only screen and (max-width: 600px) {
  .container {
    width: 100%;;
  }
}

.completed {
  text-decoration: line-through;
}
.todos {
  font-size: 1.5em;
  cursor: pointer;
}
.cardBox {
padding: 10px;
}
.removeTodoButton {
  float: right;
  text-decoration: underline;
  cursor: pointer;
  font-size: 16px;
}
.checkboxButton {
  float: left;
}
</style>