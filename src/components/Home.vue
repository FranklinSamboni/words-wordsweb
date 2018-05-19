<template>
    <div id="container" class="container" >
        <vue-word-cloud :words="words"  :color="colors">
          <template slot-scope="{word, text, weight}">
            <div style="cursor: pointer;" :title="weight" @click="onWordClick(word)">
              {{ text }}
            </div>
          </template>
      </vue-word-cloud>
    </div>  
</template>

<script>
export default {
  data() {
    return {
      words: [["romance", 19], ["horror", 3], ["fantasy", 7], ["adventure", 3]],
      colors:([, weight]) => weight > 7 ? 'SaddleBrown' : weight > 5 ? 'DarkSlateGray' : 'DimGray'
    };
  },
  created() {
    //this.getSpeeches();
  },
  methods: {
    getSpeeches() {
      axios
        .get("http://localhost:8080/audio/getSpeeches")
        .then(response => {
          console.log(response);
          this.words = response.data;
        })
        .catch(e => {
          console.log(e);
        });
    }
  }
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.container {
  width: 100%;
  height: 100%;
  padding-top: 10px;
  padding-right: 100px;
  padding-bottom: 100px;
  padding-left: 100px;
}
</style>
