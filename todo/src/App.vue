<script setup>
import { computed, ref } from 'vue';

const TODOS = ref([
  {todo:"Spor yap",
  isDone:false
  },
  {todo:"Kitap oku",
  isDone:true
  },
  {todo:"Ders çalış",
  isDone:true
  },
  {todo:"Yemek yap",
  isDone:false
  },
  {todo:"Dışarı çık",
  isDone:true
  },
  {todo:"Temizlik yap",
  isDone:false
  },
  {todo:"Kod yaz",
  isDone:false
  },
]);

const COMPLETED = computed(()=>TODOS.value.filter(todo =>todo.isDone))
const TODOLIST = computed(()=>TODOS.value.filter(todo =>!(todo.isDone)))


function handleClick(todo) {
  TODOS.value = TODOS.value.map(t=>{
    if(t.todo==todo.todo){
      t.isDone=!t.isDone;
    }
    return t
  })

}

const newTodo = ref('');

const handleNewCreateTodo=()=>{
  TODOS.value.push({todo:newTodo.value,
  isDone:false})
  newTodo.value = ('');
}





</script>

<template>
  <div class="todo-list">
    <div class="todo">
      <h2>Yapılacaklar</h2>
      <div v-for="(todo) in TODOLIST"  @click="handleClick(todo)">
      {{ todo.todo }}</div>
    </div>
    <div class="completed">
      <h2>Yapılanlar</h2>
      <div v-for="(todo) in COMPLETED" @click="handleClick(todo)">
      {{ todo.todo}}</div>
    </div>
</div>
<div class="ekle">
  <input v-model="newTodo" type="text" class="text" @keydown.enter="handleNewCreateTodo">
  <button @click="handleNewCreateTodo">ekle</button>
</div>
</template>

<style>
</style>
