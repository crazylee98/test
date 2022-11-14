<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <TodoHerder :addObj="addObj"></TodoHerder>
    <hr />
    <TodoLists :todoS="todoS" :delTodo="delTodo"></TodoLists>
    <hr />
    <TodoFooter
      :todoS="todoS"
      :allSelected="allSelected"
      :clearAllDone="clearAllDone"
    ></TodoFooter>
  </div>
</template>

<script>
import TodoHerder from "./components/TodoHerder.vue";
import TodoFooter from "./components/TodoFooter.vue";
import TodoLists from "./components/TodoLists.vue";
export default {
  name: "App",
  components: {
    TodoHerder,
    TodoFooter,
    TodoLists,
  },
  data() {
    return {
      todoS: JSON.parse(localStorage.getItem("todoS")) || [],
    };
  },
  mounted() {
    this.$bus.$on("updateTodo", this.updateTodo);
  },
  methods: {
    /**
     * 添加一个todo
     */
    addObj(obj) {
      this.todoS.unshift(obj);
    },
    /**
     * 删除一个todo
     */
    delTodo(id) {
      this.todoS = this.todoS.filter((item) => item.id !== id);
    },
    /**
     * 反选
     */
    allSelected(done) {
      this.todoS.forEach((ele) => {
        ele.choose = done;
      });
    },
    /**
     * 删除所有完成项目
     */
    clearAllDone() {
      this.todoS = this.todoS.filter((item) => !item.choose);
    },
    /**
     * 更新 编辑后的todo名字
     */
    updateTodo(id, name) {
      this.todoS.forEach((ele) => {
        if (ele.id == id) ele.todoName = name;
      });
    },
  },
  watch: {
    todoS: {
      handler(newVal) {
        localStorage.setItem("todoS", JSON.stringify(newVal));
      },
      deep: true,
    },
  },
};
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
