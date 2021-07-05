<template>
  <section class="main">
    <!-- <div>{{ $route.query.test }}</div> -->
    <input id="toggle-all" class="toggle-all" type="checkbox" />
    <label for="toggle-all">Mark all as complete</label>
    <ul class="todo-list">
      <!-- These are here just to show the structure of the list items -->
      <!-- List items should get the class `editing` when editing and `completed` when marked as completed -->
      <!-- li的completed是在字体上加上下划线 -->
      <li class="completed" v-for="(item, index) in showList" :key="index">
        <div class="view">
          <!-- 默认是checkbox选中 -->
          <input class="toggle" type="checkbox" @click="clickStatus" />
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
  name: "Active",
  data() {
    return {
      showList: [],
      //   test: this.$route.query.test,
    };
  },
  mounted() {
    console.log(this.showList);
    this.showList = this.$route.query.showList;
    // this.test = this.$route.query.test;
  },
  methods: {
    clickStatus($event, index) {
      this.showList[index].clickStatus = $event.target.checked;
      // console.log(this.all_list);
    },
  },
};
</script>

<style scoped>
@import "../../node_modules/css/index.css";
</style>