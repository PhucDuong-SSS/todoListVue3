<template>
  <TodoItem v-for="todo in todos" v-bind:key="todo.id" v-bind:todoProps="todo" />   
  
</template>
<script>
import {ref} from 'vue'
import TodoItem from './TodoItem'
export default {
    name: 'Todos',
    components : {TodoItem},
    setup()
    {
        const todos = ref([
            {
                id: 1,
                title: 'viec1',
                isComplete: false,
        },
            {
                id: 2,
                title: 'viec2',
                isComplete: false,
        },
            {
                id: 3,
                title: 'viec3',
                isComplete: true,
        }
        ])
        return {
            todos
        }    
    }
}
</script>

<style>

</style>