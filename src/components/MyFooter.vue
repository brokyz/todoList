<template>
  <div class="todo-footer">
    <label>
      <input
        type="checkbox"
        :checked="idAll"
        @change="checkAll"
        style="display: none"
      />
      <input type="checkbox" v-model="idAll" />
    </label>
    <span>
      <span>已完成 {{ doneTotal }}</span> / 全部 {{ total }}
    </span>
    <button class="btn btn-danger" @click="deleteD">清除已完成任务</button>
  </div>
</template>

<script>
  export default {
    name: "MyFooter",
    props: ["todos", "checkAllTodo", "deleteDone"],
    computed: {
      doneTotal() {
        // let i = 0;
        // this.todos.forEach(() => {
        //   i++;
        // });
        // return i;
        return this.todos.reduce((pre, todo) => pre + (todo.done ? 1 : 0), 0);
      },
      total() {
        return this.todos.length;
      },
      idAll: {
        get() {
          return this.doneTotal === this.total && this.total > 0;
        },
        set(value) {
          // this.checkAllTodo(value);
          this.$emit("checkAllTodo", value)
        }
      }
    },
    methods: {
      checkAll(e) {
        // this.checkAllTodo(e.target.checked);
        this.$emit("checkAllTodo", e.target.checked);
      },
      deleteD() {
        // this.deleteDone();
        this.$emit("deleteDone");
      }
    }
  };
</script>

<style scoped>
  /*footer*/
  .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }

  .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }

  .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }

  .todo-footer button {
    float: right;
    margin-top: 5px;
  }
</style>
