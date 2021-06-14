<template>
  <section class="main">
    <!-- <div>{{ $route.query.test }}</div> -->
    <input id="toggle-all" class="toggle-all" type="checkbox" />
    <label for="toggle-all">Mark all as complete</label>
    <ul class="todo-list">
      <!-- These are here just to show the structure of the list items -->
      <!-- List items should get the class `editing` when editing and `completed` when marked as completed -->
      <!-- li的completed是在字体上加上下划线 -->
      <li
        class="completed"
        v-for="(item, index) in $route.query.showList"
        :key="index"
      >
        <div class="view">
          <!-- 默认是checkbox选中 -->
          <input class="toggle" type="checkbox" checked />
          <label>{{ item.value }}</label>
          <button class="destroy"></button>
        </div>
        <input class="edit" value="Create a TodoMVC template" />
      </li>
      <!-- <li>
        <div class="view">
          <input class="toggle" type="checkbox" />
          <label>Buy a unicorn</label>
          <button class="destroy"></button>
        </div>
        <input class="edit" value="Rule the web" />
      </li> -->
    </ul>
  </section>
</template>
<script>
export default {
  name: "Completed",
  data() {
    return {
      showList: this.$route.query.showList,
      //   test: this.$route.query.test,
    };
  },
};
</script>

<style scoped>
@import "../../node_modules/css/index.css";
</style>