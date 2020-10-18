<template lang="html">
  <section>
    <transition-group name="list" tag="ul">
      <li v-for="(todoItem ,index) in propsdata" :key="todoItem" class="shadow">
        <i class="checkBtn fas fa-check" aria-hidden="true"></i>
        {{ todoItem }}
        <i aria-hidden="true">
          <input type="text" v-if="inputPlus == true" v-model="otherTodoItem"> </input>
        </i>
        <span class="removeBtn" type="button" @click="removeTodo(todoItem,index)">
          <i class="far fa-trash-alt" aria-hidden="true"></i>
        </span>
        <span class="updateBtn" type="button" @click="updateTodo(otherTodoItem,index)">
          <i class="far fa-trash-alt" aria-hidden="true"></i>
        </span>
      </li>
    </transition-group>
  </section>
</template>

<script>
export default {
  props:[
    'propsdata'
  ],
  data(){
    return{
      otherTodoItem : '',
      inputPlus : false
    }
  },
 methods :{
    removeTodo(todoItem,index){
      this.$emit('removeTodo',todoItem,index);
    },
    updateTodo(otherTodoItem,index){
      this.inputPlus =! this.inputPlus;
      this.$emit('updateTodo',otherTodoItem,index);
    }
  }
}
</script>

<style lang="css" scoped>
 ul{
   list-style-type: none;
   padding-left: 0px;
   margin-top: 0;
   text-align: left;
 }
 li{
   display: flex;
   min-height: 50px;
   height: 50px;
   line-height: 50px;
   margin: 0.5 rem 0;
   padding: 0 0.9rem;
   background: white;
   border-radius: 5px;

 }

 input{
   background:white;
   height: 40px;
   line-height: 50px;
   border-radius: 5px;
   border-color: gray;
   margin-left: 10px;
   font-size: 0.9rem;
 }

 .checkBtn{
   line-height: 45px;
   color: #62acde;
   margin-right: 5px;
 }
 .removeBtn{
   margin-left:  auto;
   color: #de4343;
 }
 .updateBtn{
   margin-left:  10px;
   color: black;
 }
 .list-enteer-active , .list-leave-actiove{
   transiton:all 1s;
 }
 .list-enter , .list-leave-to {
   opacity:0;
   transform:translateY(30px);
 }
</style>
