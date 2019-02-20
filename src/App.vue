<template>
  <div id="app">
    <div>
      <play2 v-for="pl in player" :key="pl.id" :imie="pl.name" v-text="pl.name"/>
      
      <button @click="removePlayer(pl.id);">Usuń</button>
    </div>
    <p />
    <button @click="addPlayer">Dodaj</button>

    <BaseInputText
      v-model="newTodoText"
      placeholder="New todo"
      @keydown.enter="addPlayer"
    />
    <ul v-if="player.length"></ul>
  </div>
</template>

<script>
import play2 from "./components/play2";
import BaseInputText from "./components/BaseInputText";

let nextTodoId = 6;

export default {
  name: "App",
  components: {
    play2,
    BaseInputText
  },
  data: function() {
    return {
      newTodoText: "",
      liczba: "5",
      player: [
        { id: 1, name: "Ewa", gra: true },
        { id: 2, name: "Jasiu", gra: true },
        { id: 3, name: "Jacek", gra: false },
        { id: 4, name: "Rogo", gra: true },
        { id: 5, name: "Partyk", gra: true }
      ]
    };
  },
  methods: {
    addPlayer() {
      const trimmedText = this.newTodoText.trim();
      if (trimmedText) {
        this.player.push({
          id: nextTodoId++,
          name: trimmedText
        });
        this.newTodoText = "";
      }
    },
    removePlayer(idToRemove) {
      this.player = this.player.filter(pl => {
        return pl.id !== idToRemove;
      });
    }
  }
};
</script>

<style></style>
