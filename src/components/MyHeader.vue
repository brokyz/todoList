<template>
  <div class="todo-header">
    <input
      type="text"
      @keyup.enter="add"
      placeholder="请输入你的任务名称，按回车键确认。双击文本修改名称。"
    />
  </div>
</template>

<script>
  import { nanoid } from "nanoid";
  export default {
    name: "Header",
    methods: {
      add(e) {
        // 检验输入框是否为空
        if (!e.target.value) return;
        // 将用户输入包装成一个对象
        const todoObj = { id: nanoid(), title: e.target.value, done: false };
        // 通知App组件去添加一个todo对象
        // this.addTodo(todoObj);
        this.$emit('addTodo', todoObj)
        // 清空输入
        e.target.value = "";
      }
    },
    props: ["addTodo"]
  };
</script>

<style scoped>
  /*header*/
  .todo-header input {
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
  }

  .todo-header input:focus {
    outline: none;
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
      0 0 8px rgba(82, 168, 236, 0.6);
  }
</style>
