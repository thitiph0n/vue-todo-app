<template>
  <div class="todo">
    <v-text-field
      class="pa-3"
      outlined
      label="Add Task"
      append-icon="mdi-plus"
      hide-details=""
      clearable
      v-model="newTaskTitle"
      @click:append="addTask"
      @keyup.enter="addTask"
    ></v-text-field>
    <v-list flat class="pt-0">
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="doneTask(task.id)"
          :class="{ 'blue lighten-5': task.isDone }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                :input-value="task.isDone"
                color="primary"
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.isDone }"
                >{{ task.title }}</v-list-item-title
              >
            </v-list-item-content>
            <v-list-item-action>
              <v-btn icon @click.stop="dialog = true">
                <v-icon color="red darken-4">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
        <v-dialog v-model="dialog" max-width="290">
          <v-card>
            <v-card-title class="headline"> Are you sure? </v-card-title>

            <v-card-text> You won't be able to revert this! </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>

              <v-btn color="greay" text @click="dialog = false"> Cancle </v-btn>

              <v-btn color="red darken-1" text @click="deleteTask(task.id)">
                Delete
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </div>
    </v-list>
  </div>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      newTaskTitle: "",
      tasks: [],
      dialog: false,
    };
  },
  methods: {
    addTask() {
      if (this.newTaskTitle.length !== 0) {
        let newTask = {
          id: Date.now(),
          title: this.newTaskTitle,
          isDone: false,
        };
        this.newTaskTitle = "";
        this.tasks.push(newTask);
      }
    },
    doneTask(id) {
      let target = this.tasks.findIndex((t) => t.id === id);
      this.tasks[target].isDone = !this.tasks[target].isDone;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((t) => t.id !== id);
      this.dialog = false;
    },
  },
  mounted() {
    if (localStorage.tasks) {
      this.tasks = JSON.parse(localStorage.tasks);
    }
  },
  watch: {
    tasks: {
      deep: true,
      handler(tasks) {
        localStorage.tasks = JSON.stringify(tasks);
      },
    },
  },
};
</script>
