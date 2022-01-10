<template>
  <div id="buylist">
    <h1>我的購物清單</h1>
    <div class="title">
      <label>產品</label>
      <input placeholder="Name" ref="input_name" />
      <label>價錢</label>
      <input type="number" min="0" placeholder="How much" ref="input_price" />
      <label>數量</label>
      <input type="number" min="0" placeholder="How many" ref="input_quantity" />
      <button class="add" @click="addList">+新增</button>
    </div>
    <div class="itemlist">
      購物清單：
      <ul>
        <li v-for="todo in todos" :class="{ active: todo.completed }" :key="todo.timestamp">
          <label class="name">{{todo.name}}</label>
          <div class="price" :value="todo.price">{{ todo.price }}</div>
          <div class="quantity" :value="todo.quantity">{{todo.quantity}}</div>
          <button class="del_btn" @click="removeList(todo)">X</button>
        </li>
        <label class="total">Total : {{getTotal}}</label>
      </ul>
    </div>
  </div>
</template>

<script>
import {reactive} from "vue";
export default {
  name: "HelloWorld",
  setup(){
    const todos = reactive([]);



    return {
      todos
    };
  },
  
  methods: {
    addList() {
      if (this.$refs.input_name.value === "") {
        alert("your name is empty ");
      } else if (this.$refs.input_quantity.value === "" || this.$refs.input_quantity.value <= 0) {
        alert("your quantity is empty or negative number");
      } else if (this.$refs.input_price.value === "" || this.$refs.input_price.value <= 0) {
        alert("your price is empty or negative number");
      } else {
        this.todos.push({
          name: this.$refs.input_name.value,
          quantity: parseInt(this.$refs.input_quantity.value),
          price: parseInt(this.$refs.input_price.value),
          timestamp: new Date().getTime()
        });
        // this.input_name.value = ""; //這邊綁model才有用
        this.$refs.input_name.value = "";
        this.$refs.input_quantity.value = "";
        this.$refs.input_price.value = "";
      }
    },
    removeList(todo) {
      this.todos.splice(this.todos.indexOf(todo), 1);
    }
  },
  computed: {
    getTotal() {
      var sum = 0;
      for (var i in this.todos) {
        sum += this.todos[i].price * this.todos[i].quantity;
      }
      return sum;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
