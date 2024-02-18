<template>
  <li>
    <label>
      <input
        type="checkbox"
        :checked="todo.isDone"
        @click="toggleChecked(todo.id)"
      />
    </label>
    <span v-show="!todo.isEdit">{{ todo.name }}</span>
    <input
      type="text"
      ref="editName"
      v-show="todo.isEdit"
      :value="todo.name"
      @blur="blurInput(todo, $event)"
    />
    <button
      class="btn btn-danger"
      @click="removeBtn(todo.id)"
    >
      删除
    </button>
    <button class="btn btn-edit" @click="editBtn(todo)">
      编辑
    </button>
  </li>
</template>

<script>
export default {
  name: 'ItemItem',
  props: ['todo'],
  methods: {
    //通知app，将isdone取反
    toggleChecked(id) {
      // this.updateTodo(id)
      this.$bus.$emit('updateTodo', id)
    },
    //删除选定todo
    removeBtn(id) {
      if (confirm('确定删除吗?')) {
        //this.deleteTodo(id)
        this.$bus.$emit('deleteTodo', id)
      }
    },
    //控制编辑,如果todo没有isEdit,则$set,否则赋值true开启编辑模式
    editBtn(todo) {
      if (todo.hasOwnProperty('isEdit')) {
        todo.isEdit = true
      } else {
        this.$set(todo, 'isEdit', true)
      }
      //editBtn自动给焦点
      //- 逻辑做成宏任务
      // setTimeout(() => this.$refs.editName.focus(), 0)
      //- $nextTick(function(){})回调函数会在"下一次dom节点更新后"执行
      //!当数据改变后,要基于更新后的dom进行某些操作时,把操作包进nextTick.      this.$nextTick(function () {
      this.$nextTick(() => {
        this.$refs.editName.focus()
      })
    },
    //input失去焦点时,通知app修改数据
    //注意标签里传参时的第二个参数@event
    blurInput(todo, e) {
      todo.isEdit = false
      if (!e.target.value.trim()) {
        return alert('输入不能为空')
      }
      this.$bus.$emit('updateName', todo.id, e.target.value)
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
