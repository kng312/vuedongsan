<template>
  <div class="black-bg" v-if="modelch == true">
    <div class="white-bg">
      <h4>상세페이지</h4>
      <p>상세페이지내용임</p>
      <button @click="modelch = false">닫기</button>
    </div>
  </div>



  <div class="menu">
    <a v-for=" (title,i) in menu" :key="i">{{title}}</a>
  </div>


  <!-- <div>
    <a :style="colorStyle" v-for="a in products" :key="a">
      <br><h4>{{ a }}</h4>
      <p>{{price1}}</p>
    </a>
  </div> -->

  <div v-for=" (a ,i) in oneroom" :key="i">
    <img :src="a.image" class="room-img">
    <h4 @click="modelch = true">{{a.title}} 원룸</h4>
    <p>{{ a.price }} 만원</p>
    <button @click="index[i]++">허위매물 신고</button> <span>신고수 : {{index[i]}}</span>
  </div>


  <!-- <div>
    <img src="./assets/room1.jpg" class="room-img">
    <h4>{{products[1]}} 원룸</h4>
    <p>{{price2}}만원</p>
    <button @click="index[1]++">허위매물 신고</button> <span>신고수 : {{index[1]}}</span>
  </div>
  <div>
    <img src="./assets/room2.jpg" class="room-img">
    <h4>{{products[2]}} 원룸</h4>
    <p>{{price2}}만원</p>
    <button @click="index[2]++">허위매물 신고</button> <span>신고수 : {{index[2]}}</span>
  </div> -->

  <div id="app">
    <h1>To-Do List</h1>
    <to-do-form @todo-added="addToDo"></to-do-form>
    <ul>
      <li v-for="item in ToDoItems" :key="item.id">
        <to-do-item :label="item.label" :done="item.done" :id="item.id"></to-do-item>
      </li>
    </ul>
  </div>
</template>

<script>
import data from './data.js';
import ToDoItem from './components/ToDoItem.vue';
import uniqueId from 'lodash.uniqueid';
import ToDoForm from './components/ToDoForm.vue';

export default {
  name: 'App',
  data(){
    return {
      oneroom : data,
      modelch : false,
      index : [0,0,0,0,0,0],
      price1 : 60,
      price2 : 70,
      colorStyle : 'color : red',
      products : ['역삼동원룸', '천호동 원룸', '마포구 원룸'],
      menu : ['Home', 'Shop', 'About'],
      ToDoItems: [
        { id: uniqueId('todo-'), label: 'Learn Vue', done: false },
        { id: uniqueId('todo-'), label: 'Create a Vue project with the CLI', done: true },
        { id: uniqueId('todo-'), label: 'Have fun', done: true },
        { id: uniqueId('todo-'), label: 'Create a to-do list', done: false }
      ]
    }
  },
  methods : {
    addToDo(toDoLabel) {
      this.ToDoItems.push({id:uniqueId('todo-'), label:toDoLabel, done:false})
    }
  },

  components: {
    ToDoItem,
    ToDoForm
  }
}
</script>

<style>
body {
  margin : 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height:100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
} 

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5;
}
.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}
</style>
