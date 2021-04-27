<template>
  <footer class="footer" v-show="todos.length">
    <span class="todo-count">
      <strong>{{todos.length}}</strong> 项目
    </span>
      <ul class="filters">
        <li><router-link to="/all" :class="{selected: filters === 'all'}" @click="handleChangeFilter('all')">All</router-link></li>
        <li><router-link to="/active" :class="{selected: filters === 'active'}" @click="handleChangeFilter('active')">Active</router-link></li>
        <li><router-link to="/completed" :class="{selected: filters === 'completed'}" @click="handleChangeFilter('completed')">Completed</router-link></li>
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
  created () {
    this.fetchFilter()
  },
  watch: {
    $route: 'fetchFilter'
  },
  computed: {
    filters () {
      return this.$store.state.filter
    },
    todosCount () {
      return this.$store.getters.todosCount
    },
    hasCompleted () {
      return this.$store.getters.hasCompleted
    }
  },
  methods: {
    handleRemoveAllCompletedTodo: function () {
      this.$store.commit('removeCompleted')
    },
    fetchFilter: function () {
      const filter = this.$route.params.filter
      this.$store.commit('changeFilter', filter)
    }
  }
}
</script>
