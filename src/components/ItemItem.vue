<template>
  <li>
    <label>
      <input
        type="checkbox"
        :checked="todo.isDone"
        @click="toggleChecked(todo.id)"
      />
      <span>{{ todo.name }}</span>
    </label>
    <button
      class="btn btn-danger"
      @click="removeBtn(todo.id)"
    >
      删除
    </button>
  </li>
</template>

<script>
export default {
  name: 'ItemItem',
  props: ['todo', 'updateTodo', 'deleteTodo'],
  methods: {
    toggleChecked(id) {
      //通知app，将isdone取反
      this.updateTodo(id)
    },
    removeBtn(id) {
      //删除选定todo
      if (confirm('确定删除吗?')) {
        this.deleteTodo(id)
      }
    },
  },
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
li:hover {
  background-color: rgb(224, 248, 210);
}
li:hover button {
  display: block;
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
</style>
