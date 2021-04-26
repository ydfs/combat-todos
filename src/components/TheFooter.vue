<template>
  <footer class="footer" v-show="todos.length">
    <span class="todo-count">
      <strong>{{todos.length}}</strong> 项目
    </span>
      <ul class="filters">
        <li><router-link to="/all" :class="{selected: filter === 'all'}" @click="handleChangeFilter('all')">All</router-link></li>
        <li><router-link to="/active" :class="{selected: filter === 'active'}" @click="handleChangeFilter('active')">Active</router-link></li>
        <li><router-link to="/completed" :class="{selected: filter === 'completed'}" @click="handleChangeFilter('completed')">Completed</router-link></li>
      </ul>
      <button class="clear-completed" v-show="hasCompleted" @click="handleRemoveAllCompletedTodo">删除已完成</button>
  </footer>
</template>

<script>
export default {
  name: 'TheFooter',
  props: {
    todos: {
      type: Array,
      default: () => []
    },
    filter: {
      type: String,
      default: 'all'
    }
  },
  computed: {
    hasCompleted () {
      return this.todos.some(data => data.completed)
    }
  },
  methods: {
    handleChangeFilter: function (filter) {
      this.$emit('update:filter', filter)
    },
    handleRemoveAllCompletedTodo: function () {
      let todos = [...this.todos]
      todos = todos.filter(data => !data.completed)
      this.$emit('update:todos', todos)
    }
  }
}
</script>
