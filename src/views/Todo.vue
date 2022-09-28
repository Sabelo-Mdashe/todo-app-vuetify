<template>
  <div>
    <v-text-field 
    @click:append="addTodo"
    @keyup.enter="addTodo"
    v-model="newTodo"
    class="pa-3"
              outlined
              label="Add Todo"
              append-icon="mdi-plus"
              hide-details
              clearable
            ></v-text-field>
    <v-list
      flat
      class="pt-0"
    >
<div v-for="todo in todos" :key="todo.id">


  <v-list-item class="pt-0" @click="doneTodo(todo.id)" :class="{'blue lighten-4': todo.done}">
    <template v-slot:default>
      <v-list-item-action>
        <v-checkbox
          :input-value="todo.done"
          color="primary"
        ></v-checkbox>
      </v-list-item-action>

      <v-list-item-content>
        <v-list-item-title :class="{'text-decoration-line-through': todo.done}">{{todo.title}}</v-list-item-title>
      </v-list-item-content>
      <v-list-item-action>
          <v-btn icon @click.stop="deleteTodo(todo.id)">
            <v-icon color="primary">mdi-delete</v-icon>
          </v-btn>
        </v-list-item-action>
    </template>
  </v-list-item>
  <v-divider></v-divider>
</div>
    </v-list>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        newTodo: '',
        todos: []
      }
    },
    methods: {
      doneTodo(id) {
        let todo = this.todos.filter(todo => todo.id === id)[0]
        todo.done = !todo.done
      },

      deleteTodo(id) {
        this.todos = this.todos.filter(todo => todo.id !== id)
      },

      addTodo() {
        let newTodo = {
          id: this.todos.length + 1,
          title: this.newTodo,
          done: false
        }

        this.todos.push(newTodo)
      }
    }
  }
</script>
