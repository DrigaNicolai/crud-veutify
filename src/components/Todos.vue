<template>
  <v-row class="mx-2 mt-6 d-flex justify-center">
    <v-col md=4 lg=8>
      <h1 class="text-h2 mb-6">List of todos</h1>
      <v-list
        two-line
      >
        <v-list-item
          v-for="todo in todos"
          :key="todo.id"
        >
          <v-list-item-content>
            <v-list-item-title>{{ todo.title }}</v-list-item-title>
            <v-list-item-subtitle>{{ todo.description }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-col>
  </v-row>
</template>
<script>
export default {
  data() {
    return {
      todos: [
        {
          id: 0,
          title: "Title 1",
          description: "Description for the element with number 1"
        },
        {
          id: 1,
          title: "Title 2",
          description: "Description for the element with number 2"
        },
        {
          id: 2,
          title: "Title 3",
          description: "Description for the element with number 3"
        },
        {
          id: 3,
          title: "Title 4",
          description: "Description for the element with number 4"
        },
        {
          id: 4,
          title: "Title 5",
          description: "Description for the element with number 5"
        }
      ]
    }
  }
}
</script>
<style>
  
</style>