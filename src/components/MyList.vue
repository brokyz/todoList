<template>
  <ul class="todo-main">
    <transition-group
      appear
      name="animate__animated animate__bounce"
      enter-active-class="animate__fadeInRight"
      leave-active-class="animate__fadeOutLeft"
    >
      <MyItem
        v-for="todoObj in todos"
        :key="todoObj.id"
        :todo="todoObj"
        :checkTodo="checkTodo"
        :deleteTodo="deleteTodo"
      ></MyItem>
    </transition-group>

    <li id="todo-tips" v-if="todos.length === 0">都做完了呢，再加一些吧！</li>
  </ul>
</template>

<script>
  import "animate.css"
  import MyItem from "./MyItem.vue"
  export default {
    name: "MyList",
    components: { MyItem },
    props: ["todos", "checkTodo", "deleteTodo"]
  }
</script>

<style scoped>
  /*main*/
  .todo-main {
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
  }

  .todo-empty {
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding-left: 5px;
    margin-top: 10px;
  }

  #todo-tips {
    text-align: center;
    list-style: none;
  }
</style>
