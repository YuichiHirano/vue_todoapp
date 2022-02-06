<template>
  <div>
    <h2>タスクリスト</h2>
    <ul>
      <li v-for="(task, index) in allTasks" :key="task.content">
        <span v-text="task.content"></span>
        <input
          type="checkbox"
          v-model="task.completed"
          @change="completeTask(index)"
        />
      </li>
    </ul>

    <div>
      <label for="changeShowCompletedTask">完了済みタスクを表示</label>
      <input
        type="checkbox"
        id="changeShowCompletedTask"
        @change="changeShowCompletedTask"
      />
    </div>

    <template v-if="getShowCompletedTask">
      <h2>完了済みタスクリスト</h2>
      <ul>
        <li v-for="(task, index) in allCompletedTasks" :key="task.content">
          <span v-text="task.content"></span>
          <input
            type="checkbox"
            v-model="task.completed"
            @change="redoTask(index)"
          />
        </li>
      </ul>
    </template>

    <label for="addTask">タスク追加</label>
    <input id="addTask" type="text" v-model="newTask" />
    <button @click="addTask">追加</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        { content: "HTML", completed: false },
        { content: "CSS", completed: false },
        { content: "JavaScript", completed: false },
        { content: "Vue.js", completed: false },
      ],
      completedTasks: [{ content: "jQuery", completed: true }],
      newTask: "",
      showCompletedTask: false,
    };
  },
  methods: {
    addTask() {
      this.tasks.push({ content: this.newTask, completed: false });
      this.newTask = "";
    },
    completeTask(index) {
      if (confirm("Are you really completed?")) {
        this.tasks.splice(index, 1);
        this.completedTasks.push(this.tasks[index]);
      }
    },
    redoTask(index) {
      if (confirm("Are you really redo?")) {
        this.completedTasks.splice(index, 1);
        this.tasks.push(this.completedTasks[index]);
      }
    },
    changeShowCompletedTask() {
      this.showCompletedTask = !this.showCompletedTask;
    },
  },
  computed: {
    allTasks() {
      return this.tasks;
    },
    allCompletedTasks() {
      return this.completedTasks;
    },
    getShowCompletedTask() {
      return this.showCompletedTask;
    },
  },
};
</script>