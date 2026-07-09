<template>
  <main class="container">
    <h1>待办事项（Vue 练习）</h1>
    <TodoList />
    <footer class="footer">这是一个练手项目 — 可以扩展排序、过滤、同步后端等功能</footer>
  </main>
</template>

<script setup>
import TodoList from './components/TodoList.vue'
</script>
