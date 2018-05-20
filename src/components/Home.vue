<template>
    
    <div id="container" class="container" >
        <!--<v-btn color="Dark" v-on:click.native="updateWords">Actualizar</v-btn>-->
        <vue-word-cloud v-bind:words="words"  :color="colors">
          <template slot-scope="{word, text, weight}">
            <div style="cursor: pointer;" :title="weight" @click="onWordClick(word)">
              {{ text }}
            </div>
          </template>
      </vue-word-cloud>
    </div>  
</template>

<script>

import { EventBus } from './event-bus.js';

export default {
  data() {
    return {
      words: [],
      colors: ([, weight]) =>
        weight > 7 ? "SaddleBrown" : weight > 5 ? "DarkSlateGray" : "DimGray"
    };
  },
  created() {
    this.updateWords();
    EventBus.$on('updateWords', (obj)=>{
      this.updateWords();
    });
  },
  methods: {
    updateWords() {
      axios
        .get("audio/getUsedWords")
        .then(response => {
          console.log(response);
          this.words = response.data.data;
        })
        .catch(e => {
          console.log(e);
        });
    },
    test() {
      this.words = [["hola", 0], ["cómo", 0], ["estás", 0]];
    }
  }
};
</script>


<style scoped>
.container {
  width: 100%;
  height: 100%;
  padding-top: 10px;
  padding-right: 10px;
  padding-bottom: 10px;
  padding-left: 10px;
}
</style>
