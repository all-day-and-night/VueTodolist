<template>
<div class="container">
  <h2>Todo List</h2>
  <div class="input-group" style="margin-bottom:10px;">
    <input type="text" class="form-control" placeholder="할일을 입력하세요" v-model="name" v-on:keyup.enter="createTodo(name)">
    <span class="input-group-btn">
      <button class="btn btn-default" type="button" @click="createTodo(name)">추가</button>
    </span>
  </div>
  <ul class="list-group">
    <li :key="index" class="list-group-item" v-for="(todo, index) in todos">
     <a href="#"> {{index+1}}. {{todo.name}}</a>
    
      <div class="btn-group pull-right" 
        style="font-size: 12px; line-height: 1;">
        <button type="button" 
        class="btn-link dropdown-toggle" 
        data-toggle="dropdown" 
        aria-haspopup="true" 
        aria-expanded="false">
          더보기<span class="caret"></span>
        </button>
        <ul class="dropdown-menu">
          <li><a href="#" @click="deleteTodo(index)">삭제</a></li>
          <li><a href="#" @click="modifyTodo(index)">수정</a></li>
        </ul>
      </div>
       <div v-if="todo.isModify" class="input-group" style="margin-bottom:10px; margin-right:60px;">
    <input  type="text" class="form-control" placeholder="수정" v-model="newTodo" v-on:keyup.enter="updateName(index, newTodo)">
    <span class="input-group-btn">
      <button class="btn btn-default" type="button" @click="updateName(index, newTodo)">수정</button>
    </span>
  </div>
    </li>
  </ul>
</div>
</template>

<script>
export default {
  name: 'TodoList',
  methods:{
    deleteTodo(i){
      this.todos.splice(i,1);
    },
    createTodo(name){
      if(name!=null){
        this.todos.push({name:name, isModify:false, newTodo:name});
        this.name=null
      }
    },
     modifyTodo(val){
      if(!this.todos[val].isModify)
      {
        this.todos[val].isModify = true;
      }
      else{
        return;
      }
    },
    updateName(index, val){
      if(val!=null){
      this.todos[index].name = val;
      this.todos[index].newTodo = val; 
      this.newTodo='';
      this.todos[index].isModify = false;
     }   
    }
  },

  data () {
    return {
      todos: [
        {
          name:'청소',
          newTodo:'청소',
          isModify:false
        },
        {
          name:'운동',
          newTodo:'운동',
          isModify:false
        },
        {
          name:'밥먹기',
          newTodo:'밥먹기',
          isModify:false
        },
        {
          name:'쉬기',
          newTodo:'쉬기',
          isModify:false
        }
      ]
    }
  }//
      //<ul>
     //<li v-if="todo.isModify" class="input-group" style="margin-bottom:10px;">
    //<input type="text" class="form-control"  placeholder="수정하세요" v-model="modifyName" v-on:keyup.enter="modifyTodo(modifyName)">
    //<span class="input-group-btn">
     // <button class="btn btn-default" type="button" @click="modifyTodo(modifyName)">수정</button>
    //</span>
    //</li>
    //</ul>

}
</script>


<style>
    
</style>