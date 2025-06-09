<template>
  <h1>Stack Linked List</h1>
  <label for="inputValue">inputValue:</label>
  <input type="text" v-model="inputValue" id="inputValue" />
  <button @click="ClickForPush">push</button>
  <button @click="ClickForPop">pop</button>
  <pre>Top:{{ stack.top() }}</pre>
  <pre>pop:{{ popValue }}</pre>
  <pre>size:{{ stack.size() }}</pre>
  <h2>
    <pre>Linked List:{{ "\n" }}{{ stack.toLinkedListString() }}</pre>
  </h2>
  <h2>
    <pre>Stack:{{ "\n" }}{{ stack.toStackString() }}</pre>
  </h2>
</template>
<script setup>
import { ref } from "vue";
const inputValue = ref("");
const popValue = ref("");
class MyNode {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
class Stack {
  constructor(stack = []) {
    this.head = null;
    this.length = 0;
    for (let i = 0; i < stack.length; i++) {
      this.push(stack[i]);
    }
  }
  toLinkedListString() {
    let myNode = this.head;
    let str = "";
    while (myNode) {
      str = str + myNode.value + "->";
      myNode = myNode.next;
    }
    return str + "null";
  }
  toStackString() {
    let myNode = this.head;
    let str = "";
    while (myNode) {
      str = str + myNode.value + "\n";
      myNode = myNode.next;
    }
    return "︻\n" + str + "︼";
  }
  push(value) {
    let myNode = new MyNode(value);
    if (this.head) {
      myNode.next = this.head;
      this.head = myNode;
    } else {
      this.head = myNode;
    }
    this.length++;
  }
  pop() {
    if (this.head) {
      const value = this.head.value;
      this.head = this.head.next;
      this.length--;
      return value;
    } else {
      return "null";
    }
  }
  top() {
    if (this.head) {
      const value = this.head.value;
      return value;
    } else {
      return "null";
    }
  }
  size() {
    return this.length;
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
