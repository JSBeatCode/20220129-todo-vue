<template>
  <div className="container">
    <HelloWorld 
      msg="TodoList"
    />
    <!-- <InsertTodo 
      @funcChange = "funcChange"
      @funcSubmit = "funcSubmit"
      @funcKeyDown = "funcKeyDown"
      :todo="state.todo"
    /> -->
    <!-- <InsertTodo 
      @funcSubmit = "funcSubmit"
      @funcKeyDown = "funcKeyDown"
      :todo="state.todo"
    /> -->
    <InsertTodo 
      @funcSubmit = "funcSubmit"
      :todo="state.todo"
    />
    <ListTodo 
      :todoList = state.todoList
      @funcDel = "funcDel"
    />
  </div>
</template>

<script>
import { onMounted, onUpdated, reactive } from 'vue';
import HelloWorld from './components/HelloWorld.vue'
import InsertTodo from './components/InsertTodo';
import { v4 as uuidv4 } from 'uuid';
import ListTodo from './components/ListTodo';

export default {
  name: 'App',
  components: {
    HelloWorld,
    InsertTodo,
    ListTodo
  },
  setup(){
    const state = reactive({
      // todo : '',
      todoList : [],
      // homePage : computed(()=>this.$route.path==='/'?true:false)
    });
    
    const funcSubmit = (val) => {
      console.log('debug3', val)

      state.todoList = [
        ...state.todoList,
        {id:uuidv4(), content:val}
      ];
      // console.log(state.todoList);
      // state.todo = '';
      // console.log("funcSubmit", state.todoList)
      // if(key===13){
      //   state.todo = '';
      // }
    }
    // const funcChange = (val) => {
    //   state.todo = val;
    //   // console.log("funcChange", state.todo)
    // }

    const funcKeyDown = () => {
      funcSubmit();
    }

    const funcDel = (id) => {
      state.todoList = state.todoList.filter(todo => id!==todo.id);
    }

    onUpdated(()=>{
      // console.log("updated", state)
    })

    onMounted(()=>{
      // console.log("mounted", state)
    })

    return {
      state,
      // funcChange,
      funcSubmit,
      funcKeyDown,
      funcDel,
      onMounted,
      onUpdated
    }
  }
}
</script>

<style>

</style>
