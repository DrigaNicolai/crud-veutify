<template>
  <v-app>
    <Header/>
    <v-main>
      <Todos/>
    </v-main>
  </v-app>
</template>

<script>
import Header from "./components/Header.vue"
import Todos from "./components/Todos.vue"

export default {
  data() {
    return {

    }
  },
  components: {
    Header,
    Todos
  }

};
</script>
