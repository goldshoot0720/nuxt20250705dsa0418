<template>
  <h1>Queue Array page</h1>
  <label for="inputValue">inputValue:</label>
  <input type="text" v-model="inputValue" id="inputValue" />
  <button @click="ClickForEnqueue">enqueue</button>
  <button @click="ClickForDequeue">dequeue</button>
  <pre>Peak:{{ queue.peak() }}</pre>
  <pre>dequeue:{{ dequeueValue }}</pre>
  <pre>size:{{ queue.size() }}</pre>
  <h2>
    <pre>Array:{{ "\n" }}{{ queue.toArrayString() }}</pre>
  </h2>
  <h2>
    <pre>▼Queue:{{ "\n" }}{{ queue.toQueueString() }}</pre>
  </h2>
</template>
<script setup>
import { ref } from "vue";
const inputValue = ref("");
const dequeueValue = ref("");
class Queue {
  constructor(queue = []) {
    this.queue = queue;
  }
  toArrayString() {
    let str = "[";
    for (let i = 0; i < this.queue.length; i++) {
      str = str + this.queue[i];
      if (i < this.queue.length - 1) {
        str = str + ",";
      }
    }
    return str + "]";
  }
  toQueueString() {
    let str = "";
    for (let i = 0; i < this.queue.length; i++) {
      str = str + this.queue[i] + " ";
    }
    return str;
  }
  enqueue(value) {
    this.queue.unshift(value);
  }
  dequeue() {
    return this.queue.shift() || "null";
  }
  peak() {
    return this.queue[0] || "null";
  }
  size() {
    return this.queue.length;
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
