<template>
  <div id="app">
    <div id="root">
      <div class="todo-container">
        <div class="todo-wrap">
          <MyHeader @addTodo="addTodo"></MyHeader>
          <MyList
            :todos="todos"
            :checkTodo="checkTodo"
            :deleteTodo="deleteTodo"
          ></MyList>
          <MyFooter
            :todos="todos"
            @checkAllTodo="checkAllTodo"
            @deleteDone="deleteDone"
          ></MyFooter>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import MyFooter from "./components/MyFooter.vue"
  import MyHeader from "./components/MyHeader.vue"
  import MyList from "./components/MyList.vue"
  export default {
    name: "App",
    components: {
      MyHeader,
      MyList,
      MyFooter
    },
    data() {
      return {
        todos: JSON.parse(localStorage.getItem("todos")) || []
      }
    },
    watch: {
      todos: {
        deep: true,
        handler(value) {
          localStorage.setItem("todos", JSON.stringify(value))
        }
      }
    },
    methods: {
      // 添加
      addTodo(todoObj) {
        // console.log("App:", todoObj);
        this.todos.unshift(todoObj)
      },
      // 控制勾选
      checkTodo(id) {
        this.todos.forEach((todo) => {
          if (todo.id === id) todo.done = !todo.done
        })
      },
      // 删除
      deleteTodo(id) {
        this.todos = this.todos.filter((todo) => {
          return todo.id !== id
        })
      },
      // 全选全不选
      checkAllTodo(done) {
        this.todos.forEach((todo) => {
          todo.done = done
        })
      },
      // 清除已完成任务
      deleteDone() {
        this.todos = this.todos.filter((todo) => {
          return !todo.done
        })
      },
      // 修改title
      changeTitle(id, newTitle) {
        this.todos.forEach((todo) => {
          if (todo.id === id) todo.title = newTitle
        })
      }
    },
    mounted() {
      this.$bus.$on("changeTitle", this.changeTitle)
    }
  }
</script>

<style>
  /*base*/
  body {
    background: #fff;
  }

  .btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
      0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }

  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
  }

  .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
  }

  .btn:focus {
    outline: none;
  }

  .todo-container {
    width: 600px;
    margin: 0 auto;
  }

  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
