<template>
  <div style="margin-bottom: 30px; text-align: center; font-size: xx-large;">Liste de Taches</div>
  <form action="" @submit.prevent="addTodo">
    <fieldset role="group">
    <input 
      v-model="newTodo"
      type="text" 
      name="" id="" 
      placeholder="Tache à effectuer">
     
    <button :disabled="newTodo.length == 0">Ajouter</button>
  </fieldset>
  </form>
<div v-if="todos.length == 0">Vous n'avez pas de taches à faire :(</div>
<div v-else>
  <ul>
    <li
    v-for="todo in sortedTodos()"
    :key="todo.date"
    :class="{completed: todo.completed}"
    >
    <label for="">
      <input type="checkbox" name="" id="" v-model="todo.completed">
      {{ todo.titre }}
    </label>
    
  </li>
  </ul>
  <label for="">
    <input type="checkbox" name="" id="" v-model="tacheFaite">
    Masquez les taches complétées
  </label>
</div>
</template>

<script setup>
import {ref} from "vue";

const tacheFaite = ref(false)
const todos = ref([])
/*const todos = ref([{
  titre: 'tache à faire',
  completed: true,
  date: 1,
},
{
  titre: 'tache de test',
  completed: false,
  date: 2,
}])*/
const newTodo =ref('')
const addTodo = () => {
  todos.value.push({
    titre: newTodo.value,
    completed: false,
    date: Date.now()
  },
)
  newTodo.value = ''
}
const sortedTodos = () => {
  const sortedTodos = todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1)
  if (tacheFaite.value == true) {
    return sortedTodos.filter(t => t.completed == false)
  }
  return sortedTodos
}
</script>

<style>
        .completed {
            opacity: .5;
            text-decoration: line-through;
        }
    </style>

