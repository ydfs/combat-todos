<template>
  <div id="app">
    <section class="todoapp" v-cloak>
      <the-header class="header" @add-todo="handleAddTodo">
        <!-- <h1>todos</h1>
        <input class="new-todo" autofocus autocomplete="off" placeholder="What needs to be done?" v-model="newTodo" @keyup.enter="handleAddTodo"> -->
      </the-header>
      <the-list :todos.sync="todos" :filter="filter"></the-list>
      <!-- <section class="main">
        <input id="toggle-all" class="toggle-all" type="checkbox" v-model="allCompleted">
        <label for="toggle-all">Mark all as complete</label>
        <ul class="todo-list">
          <li :class="['todo', {completed: todo.completed},{editing: editTodo === todo}]" v-for="(todo,index) in showTodos" :key="index">
            <div class="view">
              <input class="toggle" type="checkbox" v-model="todo.completed">
              <label @dblclick="handleEdit(todo)">{{todo.title}}</label>
              <button class="destroy" @click="handleRemoveTodo(todo)"></button>
            </div>
            <input class="edit" type="text" v-model="todo.title" v-todo-focus="editTodo === todo" @blur="handleEditDone(todo)" @keyup.enter="handleEditDone(todo)" @keyup.esc="handleEditCancel(todo)">
          </li>
        </ul>
      </section> -->
      <the-footer :todos.sync="todos" :filter.sync="filter"></the-footer>
      <!-- <footer class="footer">
        <span class="todo-count">
          <strong>3</strong> todo
        </span>
        <ul class="filters">
          <li><a href="#/all" :class="{selected: filter === 'all'}" @click="handleChangeFilter('all')">All</a></li>
          <li><a href="#/active" :class="{selected: filter === 'active'}" @click="handleChangeFilter('active')">Active</a></li>
          <li><a href="#/completed" :class="{selected: filter === 'completed'}" @click="handleChangeFilter('completed')">Completed</a></li>
        </ul>
        <button class="clear-completed" v-show="hasCompleted" @click="handleRemoveAllCompletedTodo">Clear completed</button>
      </footer> -->
    </section>
  </div>
</template>

<script>
import '@/assets/todos-html/base.css'
import '@/assets/todos-html/index.css'
import TheHeader from '@/components/TheHeader'
import TheList from '@/components/TheList'
import TheFooter from '@/components/TheFooter'
export default {
  data () {
    return {
      todos: [{
        title: '任务 一',
        completed: false
      }, {
        title: '任务 二',
        completed: true
      }, {
        title: '任务 三',
        completed: true
      }],
      editTodo: null,
      beforeEditCache: '',
      newTodo: null,
      filter: 'all'
    }
  },
  methods: {
    handleAddTodo (todo) {
      this.todos.push(todo)
    }
  },
  components: {
    'the-header': TheHeader,
    'the-list': TheList,
    'the-footer': TheFooter
  }
}
</script>
