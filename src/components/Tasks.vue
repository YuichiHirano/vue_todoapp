<template>
  <div>
    <h2>タスクリスト</h2>
    <ul>
      <li v-for="task in allTasks" :key="task.content">
        <input type="checkbox" v-model="task.completed" />
        <span v-text="task.content"></span>
      </li>
    </ul>
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
      newTask: "",
    };
  },
  methods: {
    addTask() {
      this.tasks.push({ content: this.newTask, completed: false });
      this.newTask = "";
    },
  },
  computed: {
    allTasks() {
      return this.tasks;
    },
  },
};
</script>