<template>
    <div>
        <v-list-item v-show="!isEditing">
            <template>
                <v-list-item-action>
                    <v-checkbox
                        v-model="todo.done"
                        v-on:click="changeStatus(todo)"
                    ></v-checkbox>
                </v-list-item-action>

                <v-list-item-content>
                    <v-list-item-title>{{ todo.title }}</v-list-item-title>
                    <v-list-item-subtitle>{{ todo.content }}</v-list-item-subtitle>
                </v-list-item-content>

                <v-list-item-action >
                    <v-btn icon v-on:click="deleteTodo(todo)">
                        <v-icon color="grey lighten-1">mdi-delete</v-icon>
                    </v-btn>
                </v-list-item-action>
                <v-list-item-action >
                    <v-btn icon v-on:click="showEditForm">
                        <v-icon color="grey lighten-1">mdi-pencil</v-icon>
                    </v-btn>
                </v-list-item-action>
            </template>
        </v-list-item>
      
        <v-form ref="form" v-show="isEditing">
            <v-text-field
                v-model="todo.title"
                label="Title"
            ></v-text-field>
            <v-text-field
                v-model="todo.content"
                label="Content"
            ></v-text-field>
            <v-btn class="mr-4" v-on:click="closeEditForm">Save</v-btn>
        </v-form>
        
    </div>
    
</template>

<script>
export default {
    name: 'ToDo',
    props: ['todo'],
    data() {
      return {
        isEditing: false,
      };
    },
    methods: {
      changeStatus(todo) {
          if(!todo.done){
            this.$emit('complete-todo', todo);
          }
          else{
            this.$emit('reopen-todo', todo);
          }
        
      },
      deleteTodo(todo) {
        this.$emit('delete-todo', todo);
      },
      showEditForm() {
        this.isEditing = true;
      },
      closeEditForm() {
        this.isEditing = false;
      },
    },
}
</script>