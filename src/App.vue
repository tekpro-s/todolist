<template>
  <div id="app">
    <h1 class="title">Todo List</h1>
    <div class="new">
      <input
        type="text"
        name="todo"
        id="todo"
        class="new_todo"
        v-model="newTodo"
      />
      <button class="add" @click="insertTodo">追加</button>
    </div>
    <div class="list">
      <div v-for="item in todoLists" :key="item.id" class="item">
        <input type="text" class="list_todo" v-model="item.todo" />
        <button class="update" @click="updateTodo(item.id, item.todo)">
          更新
        </button>
        <button class="delete" @click="deleteTodo(item.id)">削除</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      newTodo: "",
      todoLists: [],
    };
  },
  methods: {
    async getTodo() {
      const resData = await axios.get(
        "https://agile-brushlands-69783.herokuapp.com/api/todos"
      );
      console.log(resData);
      this.todoLists = resData.data.data;
      console.log(this.todoLists);
    },
    async insertTodo() {
      const sendData = {
        todo: this.newTodo,
      };
      await axios.post(
        "https://agile-brushlands-69783.herokuapp.com/api/todos",
        sendData
      );
      await this.getTodo();
    },
    async updateTodo(id, todo) {
      const sendData = {
        todo: todo,
      };
      await axios.put(
        "https://agile-brushlands-69783.herokuapp.com/api/todos/" + id,
        sendData
      );
      await this.getTodo();
    },
    async deleteTodo(id) {
      await axios.delete(
        "https://agile-brushlands-69783.herokuapp.com/api/todos/" + id
      );
      await this.getTodo();
    },
  },
  created() {
    this.getTodo();
  },
};
</script>

<style>
/* リセットCSS */
html,
body,
div,
span,
object,
iframe,
h1,
h2,
h3,
h4,
h5,
h6,
p,
blockquote,
pre,
abbr,
address,
cite,
code,
del,
dfn,
em,
img,
ins,
kbd,
q,
samp,
small,
strong,
sub,
sup,
var,
b,
i,
dl,
dt,
dd,
ol,
ul,
li,
fieldset,
form,
label,
legend,
table,
caption,
tbody,
tfoot,
thead,
tr,
th,
td,
article,
aside,
canvas,
details,
figcaption,
figure,
footer,
header,
hgroup,
menu,
nav,
section,
summary,
time,
mark,
audio,
video {
  margin: 0;
  padding: 0;
  border: 0;
  outline: 0;
  font-size: 100%;
  vertical-align: baseline;
  background: transparent;
}

body {
  line-height: 1;
}

article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
menu,
nav,
section {
  display: block;
}

nav ul {
  list-style: none;
}

blockquote,
q {
  quotes: none;
}

blockquote:before,
blockquote:after,
q:before,
q:after {
  content: "";
  content: none;
}

a {
  margin: 0;
  padding: 0;
  font-size: 100%;
  vertical-align: baseline;
  background: transparent;
}

/* change colours to suit your needs */
ins {
  background-color: #ff9;
  color: #000;
  text-decoration: none;
}

/* change colours to suit your needs */
mark {
  background-color: #ff9;
  color: #000;
  font-style: italic;
  font-weight: bold;
}

del {
  text-decoration: line-through;
}

abbr[title],
dfn[title] {
  border-bottom: 1px dotted;
  cursor: help;
}

table {
  border-collapse: collapse;
  border-spacing: 0;
}

/* change border colour to suit your needs */
hr {
  display: block;
  height: 1px;
  border: 0;
  border-top: 1px solid #cccccc;
  margin: 1em 0;
  padding: 0;
}

input,
select {
  vertical-align: middle;
}

html {
  background-color: white;
}
* {
  color: black;
  font-family: "Noto Sans JP";
}

/* TodoList画面CSS */
html {
  background-color: #2d197c;
}

#app {
  background-color: #fff;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%); /* 基準位置を左上から真ん中にする */
  padding: 30px 50px;
  border-radius: 30px; /* 要素の角を丸くする */
}

.title {
  font-size: 24px;
}

.new_todo {
  width: 300px;
}

.list_todo {
  width: 200px;
}

input {
  border: 1px #e7e7e7 solid;
  border-radius: 3px;
}

.new {
  display: flex;
  margin: 10px 0px;
}

.add {
  margin: 0px 0px 0px 20px;
  padding: 5px 10px; /* 上下に5px、左右に20px */
  font-weight: bold;
  color: #dc70fa;
  background: #fff;
  text-decoration: none; /* テキストのスタイルを消す */
  border: 2px #dc70fa solid; /* 境界線を引く */
  border-radius: 3px; /* 要素の角を丸くする */
}

.add:hover {
  color: #fff;
  background: #dc70fa;
}

.update {
  margin: 0px 0px 0px 60px;
  padding: 5px 10px; /* 上下に5px、左右に20px */
  font-weight: bold;
  color: #f99770;
  background: #fff;
  text-decoration: none; /* テキストのスタイルを消す */
  border: 2px #f99770 solid; /* 境界線を引く */
  border-radius: 3px; /* 要素の角を丸くする */
}

.update:hover {
  color: #fff;
  background: #f99770;
}

.delete {
  margin: 0px 0px 0px 10px;
  padding: 5px 10px; /* 上下に5px、左右に20px */
  font-weight: bold;
  color: #70fadc;
  background: #fff;
  text-decoration: none; /* テキストのスタイルを消す */
  border: 2px #70fadc solid; /* 境界線を引く */
  border-radius: 3px; /* 要素の角を丸くする */
}

.delete:hover {
  color: #fff;
  background: #70fadc;
}

.list {
  width: 400px;
}
.item {
  display: flex;
  margin: 10px 0px;
}

th {
  background: #f0e6cc;
}
</style>
