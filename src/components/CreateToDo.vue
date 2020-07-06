<template>
  <v-container>
    <v-btn icon v-on:click="openForm" v-show="!isCreating">
        <v-icon color="grey lighten-1">mdi-plus-circle</v-icon>
    </v-btn>
    <v-form ref="form" v-show="isCreating">
        <v-text-field
            v-model="titleText"
            label="Title" >
        </v-text-field>
        <v-text-field
            v-model="contentText"
            label="Content" >
        </v-text-field>
        <v-btn class="mr-4" v-on:click="sendForm()"> Save </v-btn>
        <v-btn class="mr-4" v-on:click="closeForm()"> Cancel </v-btn>
    </v-form>
  </v-container>
</template>

<script>
export default {
  name: 'CreateToDo',
  data() {
    return {
      titleText: '',
      contentText: '',
      isCreating: false,
    };
  },
  methods: {
    openForm() {
      this.isCreating = true;
    },
    closeForm() {
      this.isCreating = false;
    },
    sendForm() {
        let title;
        this.titleText == '' ? title = "New ToDo" : title = this.titleText;
        const content = this.contentText;
        this.$emit('create-todo', {
          title,
          content,
          done: false,
        });
        this.titleText = '';
        this.contentText = '';
        this.isCreating = false;
    },
  },
};
</script>