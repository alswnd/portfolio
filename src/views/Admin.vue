<template>
  <div>
    <div class="inputWrapper" v-for="(s, index) in stack" :key="index">
      <p>{{s.id}}</p>
      <input type="number" v-model="s.level" />
      <input type="text" v-model="s.description" />
      <button @click="updateBtn(index)">update</button>
    </div>

    <div class="inputWrapper">
      <input type="text" v-model="skillName" placeholder="skill name" />
      <input type="number" v-model="skillLevel" placeholder="skill level" />
      <input type="text" v-model="skillDesc" placeholder="skill description" />
      <button @click="addBtn()">add</button>
    </div>
  </div>
</template>

<script>
import { db } from "../db";

export default {
  data() {
    return {
      stack: [],
      skillName: "",
      skillLevel: "",
      skillDesc: "",
    };
  },
  firestore: {
    stack: db.collection("stack"),
  },

  methods: {
    addBtn() {
      db.collection("stack").doc(this.skillName).set({
        level: this.skillLevel,
        description: this.skillDesc,
      });
    },
    updateBtn(index) {
      console.log(index);
      console.log(this.stack[index]);
      db.collection("stack")
        .doc(this.stack[index].id)
        .update({ ...this.stack[index] });
    },
  },
};
</script>

<style>
</style>