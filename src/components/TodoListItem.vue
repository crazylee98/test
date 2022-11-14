<template>
  <div class="item_box">
    <div class="inp">
      <input type="checkbox" v-model="item.choose" />
      <span v-show="!item.canEdit">{{ item.todoName }}</span>
      <input
        type="text"
        v-show="item.canEdit"
        :value="item.todoName"
        @blur="blurHandle(item,$event)"
      />
      <button @click="delHandle(item.id)" class="btn del">删除</button>
      <button @click="editHandle(item)" class="btn edit">编辑</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoListItem",
  props: ["item", "delTodo"],
  mounted() {},
  methods: {
    /**
     * 删除该条
     */
    delHandle(id) {
      console.log(id);
      if (confirm(`是否删除该条？（${id}）`)) {
        this.delTodo(id);
      }
    },
    /**
     * 编辑
     */
    editHandle(item) {
      if (item.hasOwnProperty("canEdit")) {
        item.canEdit = true;
      } else {
        this.$set(item, "canEdit", true);
      }
    },
    /**
     * 失去焦点保存
     */
    blurHandle(item,e) {
      item.canEdit = false;
      if(!e.target.value.trim())return alert("todo不能为空哦!")
      this.$bus.$emit('updateTodo',item.id,e.target.value)
    },
  },
};
</script>e.target.value

<style lang="less" scoped>
.item_box {
  .inp {
    // width: 250px;
    height: 25px;
    text-align: center;
    margin-top: 10px;
    display: flex;

    input {
      display: block;
    }
    &:hover {
      background: rgba(0, 0, 0, 0.3);
    }
    &:hover .btn {
      display: block;
    }

    .del {
      background: red;
    }
    .edit {
      background: skyblue;
    }
  }
  .btn {
    display: none;
    margin-left: 50px;
  }
}
</style>