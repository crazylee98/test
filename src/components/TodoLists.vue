<template>
  <div class="lists_box">
    <div class="todo_items" v-for="item in todoS" :key="item.id">
      <TodoListItem :item="item" :delTodo='delTodo'></TodoListItem>
    </div>
  </div>
</template>

<script>
import TodoListItem from './TodoListItem.vue'
export default {
    name:"TodoLists",
    props:["todoS","delTodo"],
    data() {
      return {
      }
    },
    components:{
      TodoListItem
    },
}
</script>

<style>

</style>