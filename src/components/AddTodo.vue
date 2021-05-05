<template>
  <form @submit="addItem">
      <input type="text" v-model="title">
      <input type="submit" value="Them" class="btn-add">
  </form>
</template>

<script>
import {ref} from 'vue';
// import {v4 as uuidv4} from 'uuid';
export default {
name: 'AddTodo',
setup(props, content){
    const title = ref('');
    const addItem = event => {
        event.preventDefault();

        const newItem = {
            // id:uuidv4(),
            title: title.value,
            isComplete : false
        }
        content.emit('addItem', newItem)
        title.value = '';
    }
    return {
        title,
        addItem
    }
}
}
</script>

<style scoped>
    form {
        display: flex;
    }
    input[type='text'] {
        flex:10;
        padding: 5px;
    }
    input[type='submit'] {
        flex: 2;
    }
</style>