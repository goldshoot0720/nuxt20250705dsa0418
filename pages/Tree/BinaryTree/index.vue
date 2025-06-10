<template>
  <h1>Binary Tree page</h1>
  <h2>
    <pre>Binary Tree:{{ bt.toBinaryTreeString() }}</pre>
  </h2>
  <h3>PreOrder:{{ bt.PreOrder() }}</h3>
  <h3>InOrder:{{ bt.InOrder() }}</h3>
  <h3>PostOrder:{{ bt.PostOrder() }}</h3>
</template>
<script setup>
class MyNode {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
    this.height = 0;
  }
}
class BinaryTree {
  constructor() {
    this.root = null;
  }
  AddNode(value, position = [], direction = null) {
    let current = this.root;
    let myNode = new MyNode(value);
    let height = 0;
    for (let i = 0; i < position.length; i++) {
      if (position[i] === "root") {
        current = this.root;
      } else if (position[i] === "left") {
        current = current.left;
      } else if (position[i] === "right") {
        current = current.right;
      }
      height++;
    }
    myNode.height = height;
    if (direction === "root") {
      myNode.height = 0;
      this.root = myNode;
    } else if (direction === "left") {
      current.left = myNode;
    } else if (direction === "right") {
      current.right = myNode;
    }
  }
  toBinaryTreeString() {
    let height = 0;
    if (this.root) {
      let current = this.root;
      let temp = [];
      let str = "\n";
      while (current) {
        if (current.left) {
          temp.push(current.left);
        }
        if (current.right) {
          temp.push(current.right);
        }
        if (current.height > height) {
          str = str + "\n";
          height++;
        }
        str = str + " " + current.value;
        if (temp.length === 0) {
          break;
        }
        current = temp.shift();
      }
      return str;
    } else {
      return "null";
    }
  }
  PreOrder(myNode = this.root, arr = []) {
    if (!myNode) return arr;
    if (myNode.value) {
      arr.push(myNode.value);
    }
    this.PreOrder(myNode.left, arr);
    this.PreOrder(myNode.right, arr);
    return arr;
  }
  InOrder(myNode = this.root, arr = []) {
    if (!myNode) return arr;
    this.InOrder(myNode.left, arr);
    if (myNode.value) {
      arr.push(myNode.value);
    }
    this.InOrder(myNode.right, arr);
    return arr;
  }
  PostOrder(myNode = this.root, arr = []) {
    if (!myNode) return arr;
    this.PostOrder(myNode.left, arr);
    this.PostOrder(myNode.right, arr);
    if (myNode.value) {
      arr.push(myNode.value);
    }
    return arr;
  }
}

// let bt = new BinaryTree();
// bt.AddNode(1, ["root"], "root");
// bt.AddNode(2, ["root"], "left");
// bt.AddNode(3, ["root"], "right");
// bt.AddNode(4, ["root", "left"], "left");
// bt.AddNode(5, ["root", "left"], "right");
// bt.AddNode(null, ["root", "right"], "left");
// bt.AddNode(6, ["root", "right"], "right");
// bt.AddNode(7, ["root", "left", "left"], "left");
// bt.AddNode(8, ["root", "left", "left"], "right");
// bt.AddNode(9, ["root", "left", "right"], "left");
// bt.AddNode(null, ["root", "left", "right"], "right");
// bt.AddNode(10, ["root", "right", "right"], "left");
// bt.AddNode(11, ["root", "right", "right"], "right");
// bt.AddNode(12, ["root", "left", "left", "left"], "left");

let bt = new BinaryTree();
bt.AddNode("A", ["root"], "root");
bt.AddNode("B", ["root"], "left");
bt.AddNode("C", ["root"], "right");
bt.AddNode("D", ["root", "left"], "left");
bt.AddNode("E", ["root", "left"], "right");
bt.AddNode(null, ["root", "right"], "left");
bt.AddNode("F", ["root", "right"], "right");
bt.AddNode("G", ["root", "left", "left"], "left");
bt.AddNode("H", ["root", "left", "left"], "right");
bt.AddNode("I", ["root", "left", "right"], "left");
bt.AddNode(null, ["root", "left", "right"], "right");
bt.AddNode("J", ["root", "right", "right"], "left");
bt.AddNode("K", ["root", "right", "right"], "right");
bt.AddNode("L", ["root", "left", "left", "left"], "left");
</script>
