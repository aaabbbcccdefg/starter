<template>
  <section class="todo">
    <form class="add-form" @submit.prevent="addTodo">
      <input v-model="newText" placeholder="添加新任务，按回车提交" />
      <button type="submit">添加</button>
    </form>

    <ul class="list" v-if="todos.length">
      <li v-for="todo in todos" :key="todo.id" :class="{ done: todo.done }">
        <label>
          <input type="checkbox" v-model="todo.done" @change="save()" />
          <span class="text" @dblclick="startEdit(todo)" v-if="!isEditing(todo)">{{ todo.text }}</span>
          <input v-if="isEditing(todo)" class="edit-input" v-model="editText" @keyup.enter="finishEdit(todo)" @blur="finishEdit(todo)" />
        </label>
        <div class="actions">
          <button @click="startEdit(todo)">编辑</button>
          <button @click="removeTodo(todo.id)" class="danger">删除</button>
        </div>
      </li>
    </ul>

    <p v-else class="empty">还没有任务，试着添加一个 😊</p>
  </section>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue'

const LS_KEY = 'vue_todo_starter_v1'
const newText = ref('')
const todos = ref([])
const editingId = ref(null)
const editText = ref('')

onMounted(() => {
  try {
    const raw = localStorage.getItem(LS_KEY)
    todos.value = raw ? JSON.parse(raw) : []
  } catch {
    todos.value = []
  }
})

watch(todos, () => save(), { deep: true })

function save() {
  localStorage.setItem(LS_KEY, JSON.stringify(todos.value))
}

function addTodo() {
  const text = newText.value && newText.value.trim()
  if (!text) return
  todos.value.unshift({
    id: Date.now(),
    text,
    done: false
  })
  newText.value = ''
  save()
}

function removeTodo(id) {
  todos.value = todos.value.filter(t => t.id !== id)
  if (editingId.value === id) {
    editingId.value = null
    editText.value = ''
  }
  save()
}

function startEdit(todo) {
  editingId.value = todo.id
  editText.value = todo.text
  // focus handling will be natural if user clicks; could add refs for autofocus later
}

function finishEdit(todo) {
  const text = editText.value && editText.value.trim()
  if (!text) {
    // 如果编辑为空则删除该任务
    removeTodo(todo.id)
  } else {
    const item = todos.value.find(t => t.id === todo.id)
    if (item) item.text = text
    editingId.value = null
    editText.value = ''
    save()
  }
}

function isEditing(todo) {
  return editingId.value === todo.id
}
</script>

<style scoped>
.todo {
  max-width: 640px;
  margin: 0 auto;
}
.add-form {
  display:flex;
  gap:8px;
  margin-bottom:12px;
}
.add-form input {
  flex:1;
  padding:8px;
  font-size:16px;
}
.add-form button {
  padding:8px 12px;
}
.list {
  list-style:none;
  padding:0;
  margin:0;
}
.list li {
  display:flex;
  align-items:center;
  justify-content:space-between;
  padding:8px;
  border-bottom:1px solid #eee;
}
.list li.done .text {
  text-decoration:line-through;
  color:#888;
}
.actions button {
  margin-left:6px;
}
.danger { color:#b00 }
.edit-input { padding:6px; font-size:14px; width:50%; }
.empty { color:#666; text-align:center; padding:20px 0;}
</style>
