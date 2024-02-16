<template>
  <div class="todo-footer" v-show="total">
    <label>
      <!-- <input
        type="checkbox"
        :checked="isAll"
        @change="selectAll"
      />
    </label> -->
      <input type="checkbox" v-model="isAll" />
    </label>
    <span>
      <span>已完成{{ Done }}</span> /全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="clearDone">
      清除已完成任务
    </button>
  </div>
</template>

<script>
export default {
  name: 'BottomBottom',
  props: ['todos', 'deleteTodos', 'checkAllTodo'],
  computed: {
    total() {
      return this.todos.length
    },
    Done() {
      //reduce,数组长度为几则调用几次.第一次:pre = 0 ,cur = todos[0]
      return this.todos.reduce((pre, cur) => {
        return pre + (cur.isDone ? 1 : 0)
      }, 0)
    },
    isAll: {
      get() {
        return this.Done === this.total && this.total > 0
      },
      set(status) {
        this.$emit('checkAllTodo', status)
        // this.checkAllTodo(status)
      },
    },
  },
  methods: {
    clearDone() {
      if (confirm('确定删除吗?')) this.$emit('deleteTodos')
    },
  },
}
</script>

<style scoped>
/* Footer */
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
  top: 1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>
