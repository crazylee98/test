<template>
  <div class="herder_box">
    <div class="inp">
      <input
        type="text"
        placeholder="请输入"
        @keyup.enter="addName"
        v-model="title"
      />
    </div>
  </div>
</template>

<script>
import { nanoid } from "nanoid";
export default {
  name: "TodoHerder",
  props: ["addObj"],
  data() {
    return {
      title: "",
    };
  },
  methods: {
    addName() {
      if (!this.title.trim()) return alert("输入内容不能为空！");
      let obj = {
        id: nanoid(),
        todoName: this.title,
        choose: false,
      };
      this.addObj(obj);
      this.title  = "";
    },
  },
};
</script>

<style lang="less" scoped>
</style>