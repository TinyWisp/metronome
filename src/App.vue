<template>
  <div id="app">
    <div class="metronome-container">
    </div>
    <div class="row" :key=i v-for="(note, i) in notes">
      <MusicalNote :description="note.description"></MusicalNote>
    </div>
  </div>
</template>

<script>
//import Metronome from './components/Metronome.vue'
import MusicalNote from './components/MusicalNote.vue'

export default {
  name: 'app',
  components: {
    MusicalNote
  },
  mounted() {
    //this.$refs.metronome.start();
  },
  data() {
    return {
      notes: {
        '1/4': {
          description: 'stem,head hollow',
          rhymePattern: '1'
        },
        '1/4_1/4': {
          description: 'stem,head|hline one|stem,head,hline one',
          rhymePattern: '12'
        },
        '1/16_1/16_1/16_1/16': {
          description: 'stem,head|w1o3@stem,head,hline one,hline two|w1o3@stem,head,hline one,hline two|w1o3@stem,head,hline one,hline two',
          rhymePattern: '1222'
        },
        '1/12_1/12_1/12': {
          description: 'stem,head|hline one|stem,head,hline one|hline one|stem,head,hline one',
          rhymePattern: '122'
        },
        '3/16_1/16': {
          description: 'stem,head|hline one,dot|hline one|stem,head,hline one,hline two',
          rhymePattern: '1002'
        }
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.metronome-container {
  width: 100%;
  height: 100px;
  overflow: hidden;
  border: 1px solid red;
}
.row {
  display: block;
  margin-bottom: 20px;
}
</style>
