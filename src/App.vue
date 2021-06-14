<template>
  <section class="todoapp">
    <header class="header">
      <h1>todos</h1>
      <input
        class="new-todo"
        placeholder="What needs to be done?"
        autofocus
        @keyup.enter="addToDo"
      />
    </header>
    <!-- This section should be hidden by default and shown when there are todos -->
    <router-view></router-view>
    <!-- This footer should be hidden by default and shown when there are todos -->
    <footer class="footer">
      <!-- This should be `0 items left` by default -->
      <span class="todo-count"
        ><strong>{{ list_length }}</strong> item left</span
      >
      <!-- Remove this if you don't implement routing -->
      <ul class="filters">
        <li>
          <a class="selected" href="#" @click="showAll">All</a>
        </li>
        <li>
          <a href="#" @click="showActive">Active</a>
        </li>
        <li>
          <a href="#" @click="showCompleted">Completed</a>
        </li>
      </ul>
      <!-- Hidden if no completed items are left ↓ -->
      <button class="clear-completed">Clear completed</button>
    </footer>
  </section>
</template>
<script>
export default {
  name: "app",
  data() {
    return {
      // 用于渲染list，存放list用户输入的数据
      showList: [],
      list_length: 0,
      test: {
        name: "tom",
        age: 18,
      },
    };
  },
  methods: {
    addToDo($event) {
      this.showList.push({ value: $event.target.value, clickStatus: false });
      this.list_length++;
      $event.target.value = "";
      console.log(this.showList);
      this.showAll();
    },
    showAll() {
      this.$router.push({
        name: "All",
        query: {
          showList: this.showList,
          test: this.test,
        },
      });
    },
    showActive() {
      this.$router.push({
        name: "Active",
        query: {
          showList: this.showList.filter((e) => e.clickStatus == false),
        },
      });
    },
    showCompleted() {
      this.$router.push({
        name: "Completed",
        query: {
          showList: this.showList.filter((e) => e.clickStatus != true),
        },
      });
    },
  },
};
</script>
<style scoped>
@import "../node_modules/css/index.css";
</style>