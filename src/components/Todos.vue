<script>
export default {
  data() {
    return {
      modelTodo: {edit: false},
      selectOptions: ["Title", "Description"],
      selectedSort: "",
      todos: [
        {
          id: 0,
          title: "Title 1",
          description: "Description for the element with number 1",
          edit: false
        },
        {
          id: 1,
          title: "Title 2",
          description: "Description for the element with number 2",
          edit: false
        },
        {
          id: 2,
          title: "Title 3",
          description: "Description for the element with number 3",
          edit: false
        },
        {
          id: 3,
          title: "Title 4",
          description: "Description for the element with number 4",
          edit: false
        },
        {
          id: 4,
          title: "Title 5",
          description: "Description for the element with number 5",
          edit: false
        }
      ]
    }
  },
  methods: {
    createTodo() {
      const form = this.$refs.form
      if (form.validate()) {
        this.modelTodo.id = Date.now();
        this.todos.push(this.modelTodo);
        this.clearModel();
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    clearModel() {
      this.modelTodo = {edit: false};
    },
  },
  computed: {
    computedRules() {
      return {
        required: (v) => !!v || 'This is required field',
        minLength: (length) => {
          return (v) => (v && (v.length > length) )|| `Min length ${length}`;
        }
      }
    },
    /*sortedTodos() {
      if (this.selectedSort === "Title") {
        return [...this.todos].sort((todo1, todo2) => {
          return todo1.title?.localeCompare(todo2.title);
        });
      } else if (this.selectedSort === "Description") {
        return [...this.todos].sort((todo1, todo2) => {
          return todo1.description?.localeCompare(todo2.description);
        });
      } else {
        return [...this.todos];
      }
    }*/ // Works bed with delete function
  },
  watch: {
    selectedSort(newValue) {
      if (newValue === "Title") {
        this.todos.sort((todo1, todo2) => {
          return todo1.title?.localeCompare(todo2.title);
        })
      } else {
        this.todos.sort((todo1, todo2) => {
          return todo1.description?.localeCompare(todo2.description);
        })
      }
    }
  }
}
</script>
<template>
  <v-row class="mx-2 mt-6 d-flex justify-center" id="todoList">
    <v-col md=4 lg=8>
      <h1 class="text-h2 mb-6">List of todos</h1>
      <h2 class="text-h4 mb-5">Create a todo</h2>
      <v-form ref="form" lazy-validation>
        <v-text-field
          v-model="modelTodo.title"
          label="Title"
          :rules="[computedRules.required, computedRules.minLength(5)]"
        >
        </v-text-field>
        <v-text-field
          v-model="modelTodo.description"
          label="Description"
          :rules="[computedRules.required, computedRules.minLength(10)]"
        >
        </v-text-field>
        <div class="text-center d-flex justify-end">
          <v-btn
            elevation="2"
            rounded
            dark
            color="primary"
            class="mb-4"
            @click="createTodo()"
          >
            Add todo
          </v-btn>
        </div>
      </v-form>
      <v-divider></v-divider>
      <v-select
        :items="selectOptions"
        label="Select an option for sorting"
        outlined
        class="mt-4"
        v-model="selectedSort"
      >
      </v-select>
      <v-list
        two-line
        v-if="todos.length"
      >
        <v-list-item
          v-for="(todo, todoIndex) in todos"
          :key="todo.id"
        >
          <v-list-item-content>
            <div v-if="!todo.edit">
              <v-list-item-title  
                :id="todo.id+`_`+todo.title" 
                v-model="todo.title"
              >
                {{ todo.title }}
              </v-list-item-title>
              <v-list-item-subtitle 
                :id="todo.id+`_`+todo.description"
              >
                {{ todo.description }}
              </v-list-item-subtitle>
            </div>
            <div v-else>
              <v-text-field 
                dense 
                outlined 
                label="Title" 
                v-model="todo.title"
              ></v-text-field>
              <v-textarea 
                dense 
                outlined
                height="70px"
                no-resize 
                label="Description" 
                v-model="todo.description"
              ></v-textarea>
            </div>
          </v-list-item-content>
          <v-btn
            elevation="1"
            outlined
            depressed
            color="success"
            class="mr-1"
            @click.stop="todo.edit = !todo.edit"
            v-if="!todo.edit"
          >
            <v-icon left>
              mdi-pencil
            </v-icon>
            Edit
          </v-btn>
          <v-btn
            elevation="1"
            outlined
            depressed
            color="success"
            class="mr-1"
            @click.stop="todo.edit = !todo.edit"
            v-else
          >
            Save
          </v-btn>
          <v-btn
            elevation="1"
            outlined
            depressed
            color="error"
            @click="removeTodo(todoIndex)"
          >
            Remove
          </v-btn>
        </v-list-item>
      </v-list>
      <h3 v-else class="mt-4">No todos left</h3>
    </v-col>
  </v-row>
</template>
<style>
</style>