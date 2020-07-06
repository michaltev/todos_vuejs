<template>
  <v-container>

    <v-list
      subheader
      two-line
      flat
    >
      <v-subheader>Your To Do List</v-subheader>

      <v-list-item-group
        multiple
      >
          <ToDo v-on:delete-todo="deleteTodo" 
                v-on:complete-todo="completeTodo" 
                v-on:reopen-todo="reopenTodo"
                v-for="(todo, i) in todos" 
                :key="i" 
                :todo.sync="todo"/>

      </v-list-item-group>
    </v-list>


    <CreateToDo v-on:create-todo="createTodo"/>
  </v-container>
</template>

<script>
import ToDo from './ToDo';
import CreateToDo from './CreateToDo';
export default {
  name: 'ToDoList',
  components: {
    ToDo,
    CreateToDo
  },
  data() {
    return {
      todos: [{
          title: 'walk the dog',
          done: false,
          content: 'lucky needs to wlk 5 km a day',
        },
        {
          title: 'water the flowers',
          done: false,
          content: 'roses are red and love water',
        },
        {
          title: 'clean the kitchen',
          done: true,
          content: 'stove too!',
        }]
  };
},
  methods: {
    deleteTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    createTodo(newTodo) {
      this.todos.push(newTodo);
    },
    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
    },
    reopenTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = false;
    },
  },
  }
</script>
