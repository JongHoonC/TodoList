<template>
  <h3>TodoList</h3>
  <div class="wrap">
    <div class="inputbox">
      <input type="date" v-model="todoDate" name="" id="date" />
      <input type="text" v-model="todoItem" id="text" @keyup.enter="addTodo" />
      <button type="submit" @click="addTodo">+</button>
    </div>
    <ul>
      <li
        v-for="(todo, index) in todolist"
        :key="todo"
        v-bind:class="{ completed: todo.complete }"
        @click="complete(todo, index)"
      >
        {{ todo.dates }}에는 {{ todo.item }} 을(를) 할 예정입니다.
        <button @click="removeTodo(todo, index)">
          <span>-</span>
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      todoDate: "",
      todoItem: "",
      todolist: [],
    };
  },
  methods: {
    addTodo: function () {
      console.log(this.todoItem);
      if (this.todoItem != null) {
        const obj = {
          dates: this.todoDate,
          item: this.todoItem,
          complete: false,
        };
        localStorage.setItem(this.todoItem, JSON.stringify(obj));
        console.log(obj);
        this.todolist.push(obj);
        this.todoItem = "";
      }
    },
    removeTodo: function (todo, index) {
      localStorage.removeItem(todo.item);
      this.todolist.splice(index, 1);
    },
    complete: function (todo, index) {
      todo.complete = !todo.complete; //obj 에 있는 false 를 true로 바꿔주는 구문
      localStorage.removeItem(todo.item);
      localStorage.setItem(todo.complete, JSON.stringify(todo));
    },
  },
  //중요 표시를 하기 위한 구문
  created: function () {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
          this.todolist.push(
            JSON.parse(localStorage.getItem(localStorage.key(i)))
          );
        }
      }
    }
  },
};
</script>

<style scoped>
h3 {
  font-size: 60px;
  text-align: center;
  font-weight: bold;
}
li {
  list-style: none;
  margin: 6px 0;
  text-align-last: left;
  display: flex;
  justify-content: space-between;
}
.completed {
  width: auto;
  color: #f00;
  cursor: pointer;
  text-decoration: line-through;
}

.wrap {
  width: 500px;
  margin: 0 auto;
  margin-top: 150px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
#date {
  font-family: inherit;
}
#text {
  font-family: inherit;
  margin-left: 30px;
}
input {
  outline: none;
  background-color: transparent;
  border: 1px solid #333333;
  padding: 5px 20px;
  box-sizing: border-box;
  border-radius: 20px;
}
button {
  border: none;
  background-color: #42b983;
  width: 30px;
  height: 30px;
  box-sizing: border-box;
  margin-left: 10px;
  color: #f2f2f2;
  border-radius: 1000px;
  text-align: center;
  position: relative;
}
button > span {
  position: absolute;
  top: 20%;
  left: 50%;
  transform: translate(-50%);
  display: block;
}
.inputbox {
  display: flex;
  justify-content: space-between;
}
.inputbox > button {
  background-color: rgb(206, 96, 46);
}
</style>
