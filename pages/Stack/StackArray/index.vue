<template>
  <h1>Stack Array page</h1>
  <label for="inputValue">inputValue:</label>
  <input type="text" v-model="inputValue" id="inputValue" />
  <button @click="ClickForPush">push</button>
  <button @click="ClickForPop">pop</button>
  <pre>Top:{{ stack.top() }}</pre>
  <pre>pop:{{ popValue }}</pre>
  <pre>size:{{ stack.size() }}</pre>
  <h2>
    <pre>Array:{{ "\n" }}{{ stack.toArrayString() }}</pre>
  </h2>
  <h2>
    <pre>Stack:{{ "\n" }}{{ stack.toStackString() }}</pre>
  </h2>
</template>
<script setup>
import { ref } from "vue";
const inputValue = ref("");
const popValue = ref("");
class Stack {
  constructor(stack = []) {
    this.stack = stack;
  }
  toArrayString() {
    let str = "[";
    for (let i = 0; i < this.stack.length; i++) {
      str = str + this.stack[i];
      if (i < this.stack.length - 1) {
        str = str + ",";
      }
    }
    return str + "]";
  }
  toStackString() {
    let str = "";
    for (let i = 0; i < this.stack.length; i++) {
      str = this.stack[i] + "\n" + str;
    }
    return "︻\n" + str + "︼";
  }
  push(value) {
    unshift();
  }
  pop() {
    return this.stack.pop() || "null";
  }
  top() {
    return this.stack[this.stack.length - 1] || "null";
  }
  size() {
    return this.stack.length;
  }
}
const stack = ref(new Stack(Array.from({ length: 37 }, (_, i) => i + 1)));
function ClickForPush() {
  if (inputValue.value) {
    stack.value.push(inputValue.value);
    inputValue.value = "";
  }
}
function ClickForPop() {
  popValue.value = stack.value.pop();
}
</script>
