<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <TopTop @getNewTodo="getNewTodo" />
        <ItemsItems
          :todos="todos"
          :updateTodo="updateTodo"
          :deleteTodo="deleteTodo"
        />
        <BottomBottom
          :todos="todos"
          @checkAllTodo="checkAllTodo"
          @deleteTodos="deleteTodos"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TopTop from './components/TopTop'
import ItemsItems from './components/ItemsItems'
import BottomBottom from './components/BottomBottom'

export default {
  name: 'App',
  data() {
    return {
      todos:
        //* 如果local本地没有获取到数据，则值为null
        JSON.parse(localStorage.getItem('todos')) || [],
    }
  },
  watch: {
    todos: {
      deep: true,
      handler(value) {
        localStorage.setItem('todos', JSON.stringify(value))
      },
    },
  },
  components: { TopTop, ItemsItems, BottomBottom },
  methods: {
    //新增todo
    getNewTodo(todo) {
      this.todos.unshift(todo)
    },
    //删除todo
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => {
        return todo.id !== id
      })
    },
    //删除已完成的todo
    deleteTodos() {
      this.todos = this.todos.filter((todo) => {
        return !todo.isDone
      })
    },
    //修改todo
    //!死了妈了改这个bug改了一小时我操死你的吗
    //?收获:要缩小错误范围
    updateTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) {
          todo.isDone = !todo.isDone
        }
      })
    },
    //全选todo
    checkAllTodo(done) {
      //遍历每一个小框，将小框的true或false和全选框的选择状态同步
      this.todos.forEach((todo) => {
        todo.isDone = done
      })
    },
  },
}
</script>

<style>
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
