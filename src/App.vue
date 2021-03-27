<template>
  <v-app id="inspire">
    <v-app-bar
      app
      prominent
      absolute
      color="primary"
      dark
      src="@/assets/nav-bg.jpg"
    >
      <v-toolbar-title class="pl-5 text-h4">Todo App</v-toolbar-title>
      <v-spacer></v-spacer>

      <a
        href="https://github.com/thitiph0n/vue-todo-app"
        style="text-decoration: none"
      >
        <v-btn icon>
          <v-icon>mdi-github</v-icon>
        </v-btn></a
      >
    </v-app-bar>

    <v-main>
      <v-card flat class="mx-auto px-2 py-0 ma-1" max-width="960">
        <Todo />
      </v-card>
    </v-main>
  </v-app>
</template>

<script>
import Todo from "./components/Todo.vue";

export default {
  components: {
    Todo,
  },
};
</script>