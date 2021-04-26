<template>
  <header class="header">
    <h1>todos</h1>
    <input class="new-todo" autofocus autocomplete="off" placeholder="需要做什么呢 ？" v-model="newTodo" @keyup.enter="addTodo">
  </header>
</template>

<script>
export default {
  name: 'TheHeader',
  props: {
    todos: {
      type: Array,
      default: () => []
    }
  },
  data () {
    return {
      newTodo: ''
    }
  },
  methods: {
    addTodo: function () {
      this.$emit('add-todo', {
        title: this.newTodo,
        completed: false
      })
      this.newTodo = ''
    }
  }
}
</script>
