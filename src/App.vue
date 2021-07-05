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
    <!-- <router-view :showList="showList" :test="test"></router-view> -->
    <section class="main">
      <!-- <div>{{ $route.query.test }}</div> -->
      <input
        id="toggle-all"
        class="toggle-all"
        type="checkbox"
        @click="toggleAll"
      />
      <label for="toggle-all">Mark all as complete</label>
      <ul class="todo-list">
        <!-- These are here just to show the structure of the list items -->
        <!-- List items should get the class `editing` when editing and `completed` when marked as completed -->
        <!-- li的completed是在字体上加上下划线 -->
        <li
          :class="item.clickStatus ? 'completed' : ''"
          v-for="(item, index) in viewList"
          :key="index"
        >
          <div class="view">
            <!-- 默认是checkbox选中 -->
            <input
              class="toggle"
              type="checkbox"
              :checked="viewList[index].clickStatus"
              @click="clickStatus($event, index)"
            />
            <label>{{ item.value }}</label>
            <button class="destroy" @click="deleteList(index)"></button>
          </div>
          <input class="edit" value="Create a TodoMVC template" />
        </li>
      </ul>
    </section>
    <!-- This footer should be hidden by default and shown when there are todos -->
    <footer class="footer" v-if="showList.length">
      <!-- This should be `0 items left` by default -->
      <span class="todo-count"
        ><strong>{{ list_length }}</strong> item left</span
      >
      <!-- Remove this if you don't implement routing -->
      <ul class="filters">
        <li>
          <a class="selected" href="javascript:;" @click="showAll">All</a>
        </li>
        <li>
          <a href="javascript:;" @click="showActive">Active</a>
        </li>
        <li>
          <a href="javascript:;" @click="showCompleted">Completed</a>
        </li>
      </ul>
      <!-- Hidden if no completed items are left ↓ -->
      <button class="clear-completed" @click="clearCompleted">
        Clear completed
      </button>
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
      viewList: [],
      list_length: 0,
      test: {
        name: "tom",
        age: 18,
      },
    };
  },
  methods: {
    addToDo($event) {
      console.log(this.showList);
      this.showList.push({ value: $event.target.value, clickStatus: false });
      this.list_length++;
      $event.target.value = "";
      this.viewList = this.showList;

      // console.log(this.showList);
      // this.showAll();
    },
    clickStatus($event, index) {
      this.showList[index].clickStatus = $event.target.checked;
      console.log(this.showList);
    },
    showAll() {
      this.$router.push({ name: "All" });
      // this.$router.push({
      //   name: "All",
      //   // query: {
      //   //   showList: this.showList,
      //   //   // test: this.test,
      //   // },
      // });
      this.viewList = this.showList;
    },
    showActive() {
      this.$router.push({ name: "Active" });

      // this.$router.push({
      //   name: "Active",
      //   // query: {
      //   //   showList: this.showList.filter((e) => e.clickStatus == false),
      //   // },
      // });
      this.viewList = this.showList.filter((e) => e.clickStatus == false);
    },
    showCompleted() {
      this.$router.push({ name: "Completed" });

      // this.$router.push({
      //   name: "Completed",
      //   query: {
      //     showList: this.showList.filter((e) => e.clickStatus != true),
      //   },
      // });
      this.viewList = this.showList.filter((e) => e.clickStatus == true);
    },
    // 删除标签
    deleteList(index) {
      this.showList.splice(index, 1);
      this.list_length--;
    },
    // 删除已经完成的list
    clearCompleted() {
      this.showList = this.showList.filter((e) => !e.clickStatus == true);
      this.viewList = this.showList;
      this.list_length = this.viewList.length;
    },
    // 全选
    toggleAll() {
      if (this.showList.every((e) => e.clickStatus == true)) {
        this.showList.forEach((e) => (e.clickStatus = false));
      } else {
        this.showList.forEach((e) => (e.clickStatus = true));
      }
      this.viewList = this.showList;
    },
  },
};
</script>
<style scoped>
@import "../node_modules/css/index.css";
</style>