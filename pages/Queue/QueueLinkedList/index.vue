<template>
  <h1>Queue Linked List</h1>
  <label for="inputValue">inputValue:</label>
  <input type="text" v-model="inputValue" id="inputValue" />
  <button @click="ClickForEnqueue">enqueue</button>
  <button @click="ClickForDequeue">dequeue</button>
  <pre>Peak:{{ queue.peak() }}</pre>
  <pre>dequeue:{{ dequeueValue }}</pre>
  <pre>size:{{ queue.size() }}</pre>
  <h2>
    <pre>Linked List:{{ "\n" }}{{ queue.toLinkedListString() }}</pre>
  </h2>
  <h2>
    <pre>▼Queue:{{ "\n" }}{{ queue.toQueueString() }}</pre>
  </h2>
</template>
<script setup>
import { ref } from "vue";
const inputValue = ref("");
const dequeueValue = ref("");
class MyNode {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
class Queue {
  constructor(queue = []) {
    this.head = null;
    this.length = 0;
    for (let i = 0; i < queue.length; i++) {
      this.enqueue(queue[i]);
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
  toQueueString() {
    let myNode = this.head;
    let str = "";
    while (myNode) {
      str = str + myNode.value + " ";
      myNode = myNode.next;
    }
    return str;
  }
  enqueue(value) {
    let myNode = new MyNode(value);
    if (this.head) {
      let curr = this.head;
      while (curr.next) {
        curr = curr.next;
      }
      curr.next = myNode;
    } else {
      this.head = myNode;
    }
    this.length++;
  }
  dequeue() {
    if (this.head) {
      const value = this.head.value;
      this.head = this.head.next;
      this.length--;
      return value;
    } else {
      return "null";
    }
  }
  peak() {
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
const queue = ref(new Queue(Array.from({ length: 37 }, (_, i) => i + 1)));
function ClickForEnqueue() {
  if (inputValue.value) {
    queue.value.enqueue(inputValue.value);
    inputValue.value = "";
  }
}
function ClickForDequeue() {
  dequeueValue.value = queue.value.dequeue();
}
</script>
