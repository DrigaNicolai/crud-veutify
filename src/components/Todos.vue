<template>
  <v-row class="mx-2 mt-6 d-flex justify-center" id="todoList">
    <v-col md=4 lg=8>
      <h1 class="text-h2 mb-6">List of todos</h1>
      <v-form>
        <h2 class="text-h4 mb-5">Create a todo</h2>
        <v-text-field
          v-model="title"
          label="Title"
          required
        >
        </v-text-field>
        <v-text-field
          v-model="description"
          label="Description"
          required
        >
        </v-text-field>
        <div class="text-center d-flex justify-end">
          <v-btn
            elevation="2"
            rounded
            dark
            color="primary"
            class="mb-4"
            @click="createTodo"
          >
            Add todo
          </v-btn>
        </div>
      </v-form>
      <v-divider></v-divider>
      <v-list
        two-line
        v-if="todos.length"
      >
        <v-list-item
          v-for="todo in todos"
          :key="todo.id"
        >
          <v-list-item-content>
            <v-list-item-title @click="editTodo(todo, 1)" :id="todo.id+`_`+todo.title">{{ todo.title }}</v-list-item-title>
            <v-list-item-subtitle 
              @click="editTodo(todo, 2)" 
              :id="todo.id+`_`+todo.description"
            >
              {{ todo.description }}
            </v-list-item-subtitle>
          </v-list-item-content>
          <v-btn
            elevation="1"
            outlined
            depressed
            color="error"
            @click="removeTodo(todo)"
          >
            Remove
          </v-btn>
        </v-list-item>
      </v-list>
      <h3 v-else class="mt-4">No todos left</h3>
    </v-col>
  </v-row>
</template>
<script>
export default {
  data() {
    return {
      title: "",
      description: "",
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
  },
  methods: {
    createTodo() {
      if (this.title && this.description) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          description: this.description
        };
        this.todos.push(newTodo);
        this.title = "";
        this.description = "";
      }
    },
    removeTodo(todo) {
      this.todos = this.todos.filter(t => t.id !== todo.id)
    },
    editTodo(todo, n) {
      let view = null;
      if (n === 1) {
        console.log("Title");
        view = document.getElementById(`${todo.id}_${todo.title}`);
      } else {
        console.log("Description");
        view = document.getElementById(`${todo.id}_${todo.description}`);
      }
      const area = document.createElement("textarea");
      area.className = "edit";
      area.value = view.innerText;
      area.addEventListener("keydown", (event) => {
        if(event.key == "Enter") {
          area.blur();
        }
      });
      area.addEventListener("blur", () => {
        view.innerText = area.value;
        area.replaceWith(view);
      });
      view.replaceWith(area);
      area.focus();
    }
  }
}
</script>
<style>
 .edit {
   border: 4px solid green;
 }
</style>