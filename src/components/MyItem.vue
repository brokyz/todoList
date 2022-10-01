<template>
  <li>
    <input
      type="checkbox"
      :checked="todo.done"
      @change="handleCheck(todo.id)"
    />
    <!-- <input type="checkbox" v-model="todo.done" /> -->
    <span v-show="!isEdit" id="title" @dblclick="edit"> {{ todo.title }}</span>
    <input
      id="editor"
      v-show="isEdit"
      @blur="saveEdit(todo.id, $event)"
      type="text"
      ref="input"
    />
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
  </li>
</template>

<script>
  export default {
    name: "MyItem",
    props: ["todo", "checkTodo", "deleteTodo"],
    data() {
      return {
        isEdit: false
      }
    },
    methods: {
      handleCheck(id) {
        this.checkTodo(id)
      },
      handleDelete(id) {
        this.deleteTodo(id)
      },
      edit() {
        this.isEdit = true
        // console.log(this.$refs.input)
        this.$nextTick(() => {
          this.$refs.input.focus()
        })
      },
      saveEdit(id, e) {
        this.isEdit = false
        // console.log(id, e.target.value)
        if (e.target.value != "")
          this.$bus.$emit("changeTitle", id, e.target.value)
      }
    }
  }
</script>

<style scoped>
  /*item*/
  li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
  }

  li label {
    float: left;
    cursor: pointer;
  }

  li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
  }

  li button {
    float: right;
    display: none;
    margin-top: 3px;
  }

  li:before {
    content: initial;
  }

  li:last-child {
    border-bottom: none;
  }

  li:hover {
    background-color: #ddd;
  }

  li:hover button {
    display: block;
  }

  #editor {
    outline: none;
    border: 1px solid #ccc;
  }

  input:focus {
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
      0 0 8px rgba(82, 168, 236, 0.6);
  }
</style>
