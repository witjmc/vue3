<template>
  <div id="app" class="container">
    <div class="card card-body bg-light">
      <div class="title">:: Todolist App</div>
    </div>
    <div class="card card-default card-borderless">
      <div class="card-body">
        <InputTodo @add-todo="addTodo" />
        <!--addTodo 함수-->
        <TodoList
          :todoList="todoList"
          @delete-todo="deleteTodo"
          @toggle-completed="toggleCompleted"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import TodoList from './components/TodoList.vue'
import InputTodo from './components/InputTodo.vue'
import { ref, provide } from 'vue'

//const ts = new Date().getTime()
/*
const todoList = ref([
  { id: ts, todo: '자전거 타기', completed: false },
  { id: ts + 2, todo: '공부 하기', completed: false },
  { id: ts + 3, todo: '놀기 하기', completed: false }
])

emit 하려고 선언한 데이터인데, 추가 삭제 작동되지 않아서 provide, inject를 사용
*/

const todoList = ref([])

const addTodo = (todo) => {
  if (todo.length >= 2) {
    console.log('부모컴포넌트', todo)
    todoList.value.push({ id: new Date().getTime(), todo: todo, completed: false })
  }
}

provide('todoList', todoList)
provide('addTodo', addTodo)

const deleteTodo = (id) => {
  const index = todoList.value.findIndex((item) => id === item.id)
  if (index !== -1) {
    todoList.value.splice(index, 1)
  }
}

const toggleCompleted = (id) => {
  const index = todoList.value.findIndex((item) => id === item.id)
  if (index !== -1) {
    todoList.value[index].completed = !todoList.value[index].completed
  }
}
</script>
