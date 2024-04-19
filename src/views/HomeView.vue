<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="To-Do App"/>
    <ToDoList/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue';
import ToDoList from '@/components/ToDoList.vue';

export default {
  name: 'HomeView',
  components: {
    HelloWorld,
    ToDoList
  }
}
</script>
