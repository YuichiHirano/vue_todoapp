<template>
  <v-app>
    <v-toolbar color="indigo" dark max-height="64px">
      <v-toolbar-title>タスクリスト</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
    </v-toolbar>
    <v-card
      v-for="(task, index) in allTasks"
      :key="task.content"
      outlined
      elevation="1"
      max-width="344"
    >
      <v-card-text>
        <p class="text-h4 text--primary">
          {{ task.content }}
        </p>
        <div class="text--primary">
          {{ task.detail }}
        </div>
      </v-card-text>
      <v-card-actions>
        <v-btn color="blue darken-1" text @click="finishedTask(index)">
          FINISHED
        </v-btn>
      </v-card-actions>
    </v-card>

    <v-card elevation="1" max-width="344">
      <v-card-text>
        <v-text-field v-model="task.content" label="title"></v-text-field>
        <v-text-field v-model="task.detail" label="detail"></v-text-field>
      </v-card-text>
      <v-card-actions>
        <v-btn color="primary" @click="addTask">ADD</v-btn>
      </v-card-actions>
    </v-card>

    <div>
      <label for="changeShowfinishedTask">SHOW FINISHED</label>
      <input
        type="checkbox"
        id="changeShowfinishedTask"
        @change="changeShowfinishedTask"
      />
    </div>

    <template v-if="getShowfinishedTask">
      <v-card
        v-for="task in allfinishedTasks"
        :key="task.content"
        outlined
        disabled
        elevation="2"
        max-width="344"
      >
        <v-card-text>
          <p class="text-h4 text--primary">
            {{ task.content }}
          </p>
          <div class="text--primary">
            {{ task.detail }}
          </div>
        </v-card-text>
      </v-card>
    </template>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        { content: "HTML", detail: "書籍Aを読む", finished: false },
        { content: "CSS", detail: "web講座Bを受講", finished: false },
        { content: "JavaScript", detail: "", finished: false },
        { content: "Vue.js", detail: "研修Cを受講", finished: false },
      ],
      finishedTasks: [{ content: "jQuery", detail: "", finished: true }],
      task: {
        content: "",
        detail: "",
        finished: false,
      },
      showfinishedTask: false,
    };
  },
  methods: {
    addTask() {
      this.tasks.push(this.task);
      this.task = {
        content: "",
        detail: "",
        finished: false,
      };
    },
    finishedTask(index) {
      if (confirm("Are you really finished?")) {
        const task = this.tasks.splice(index, 1)[0];
        task.finished = true;
        this.finishedTasks.push(task);
      }
    },
    redoTask(index) {
      if (confirm("Are you really redo?")) {
        const task = this.finishedTasks.splice(index, 1)[0];
        task.finished = false;
        this.tasks.push(task);
      }
    },
    changeShowfinishedTask() {
      this.showfinishedTask = !this.showfinishedTask;
    },
  },
  computed: {
    allTasks() {
      return this.tasks;
    },
    allfinishedTasks() {
      return this.finishedTasks;
    },
    getShowfinishedTask() {
      return this.showfinishedTask;
    },
  },
};
</script>