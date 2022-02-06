<template>
  <div>
    <h2>タスクリスト</h2>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        <input type="checkbox" v-model="task.completed" />
        <span v-text="task.content"></span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        { id: 0, content: "HTML", completed: false },
        { id: 1, content: "CSS", completed: false },
        { id: 2, content: "JavaScript", completed: false },
        { id: 3, content: "Vue.js", completed: false },
      ],
    };
  },
};
</script>