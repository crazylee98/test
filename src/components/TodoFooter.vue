<template>
  <div class="footer_b0x" >
    <div v-if="todoS.length">
      <input type="checkbox" v-model="allDone" />
      <span>已完成{{ doneTodo }} / 全部{{ todoS.length }} </span>
      <button @click="delAllDone">删除全部已完成</button>
    </div>
    <div class="noHas" v-else>没有TODO哦!</div>
  </div>
</template>

<script>
export default {
  name: "TodoFooter",
  props: ["todoS",'allSelected','clearAllDone'],
  computed: {
    doneTodo() {
      return this.todoS.reduce((pre, current) => {
        return pre + (current.choose ? 1 : 0);
      }, 0);
    },
    allDone:{
      get(){
        return this.doneTodo == this.todoS.length && this.todoS.length != 0;
      },
      set(val){
        console.log(val);
        this.allSelected(val)
      }
    }
  },
  methods: {
    /** 
     * 删除完成项
     */
    delAllDone(){
      this.clearAllDone()
    }
  },
};
</script>

<style lang="less" scoped>
</style>