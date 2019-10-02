<template>
  <div id="app">
    <div class="metronome-container">
    </div>
    <div class="rp-row" :key=i v-for="(row, i) in rhymePatternLayout">
      <div class="rp-col" :style="{width: 100 / row.length + '%'}" :key=j v-for="(rp, j) in row">
        <MusicalNote :description="description" :key=k v-for="(description, k) in notes[rp]['descriptions']"></MusicalNote>
      </div>
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
          descriptions: ['stem,head'],
          rhymePattern: '1'
        },
        '1/8_1/8': {
          descriptions: ['stem,head|hline one|hline  one|stem,head,hline one'],
          rhymePattern: '12'
        },
        '1/16_1/16_1/16_1/16': {
          descriptions: ['stem,head|w1o3@stem,head,hline one,hline two|w1o3@stem,head,hline one,hline two|w1o3@stem,head,hline one,hline two'],
          rhymePattern: '1222'
        },
        '1/16_1/16_1/16_1/16_1/4': {
          descriptions: ['stem,head|w1o3@stem,head,hline one,hline two|w1o3@stem,head,hline one,hline two|w1o3@stem,head,hline one,hline two', 'stem,head'],
          rhymePattern: '1222'
        },
        '1/12_1/12_1/12': {
          descriptions: ['tuple t3>stem,head|hline one|stem,head,hline one|hline one|stem,head,hline one'],
          rhymePattern: '122'
        },
        '1/12_1/12_1/12_1/4': {
          descriptions: ['tuple t3>stem,head|hline one|stem,head,hline one|hline one|stem,head,hline one', 'stem,head'],
          rhymePattern: '122,1'
        },
        '1/20_1/20_1/20_1/20_1/20': {
          descriptions: ['tuple t5>stem,head|w1o5@hline one,stem,head|w1o5@hline one,stem,head|w1o5@hline one,stem,head|w1o5@hline one,stem,head'],
          rhymePaterrn: '12222'
        },
        '1/20_1/20_1/20_1/20_1/20_1/4': {
          descriptions: ['tuple t5>stem,head|w1o5@hline one,stem,head|w1o5@hline one,stem,head|w1o5@hline one,stem,head|w1o5@hline one,stem,head', 'stem,head'],
          rhymePaterrn: '12222,1'
        },
        '3/16_1/16': {
          descriptions: ['stem,head|hline one,dot|hline one|stem,head,hline one,hline two'],
          rhymePattern: '1002'
        },
        '3/16_1/16_1/4': {
          descriptions: ['stem,head|hline one,dot|hline one|stem,head,hline one,hline two', 'stem,head'],
          rhymePattern: '1002,1'
        },
        '1/16_3/16': {
          descriptions: ['stem,head|hline one,hline two|w1o5@hline one,stem,head|dot'],
          rhymePattern: '1200'
        },
        '1/16_3/16_1/4': {
          descriptions: ['stem,head|hline one,hline two|w1o5@hline one,stem,head|dot', 'stem,head'],
          rhymePattern: '1200,1'
        },
        '1/8_1/16_1/16': {
          descriptions: ['stem,head|w1o5@stem,head,hline one|w1o5@stem,head,hline one,hline two'],
          rhymePattern: '1022'
        },
        '1/8_1/16_1/16_1/4': {
          descriptions: ['stem,head|w1o5@stem,head,hline one|w1o5@stem,head,hline one,hline two', 'stem,head'],
          rhymePattern: '1022,1'
        },
        '1/16_1/16_1/8': {
          descriptions: ['stem,head|w1o5@stem,head,hline one, hline two|w1o5@stem,head,hline one'],
          rhymePattern: '1220'
        },
        '1/16_1/16_1/8_1/4': {
          descriptions: ['stem,head|w1o5@stem,head,hline one, hline two|w1o5@stem,head,hline one', 'stem,head'],
          rhymePattern: '1220,1'
        },
        '1/16_1/8_1/16': {
          descriptions: ['stem,head|hline one,hline two|w1o5@hline one,stem,head|w1o5@hline one|hline one,hline two,stem,head'],
          rhymePattern: '1202'
        },
        '1/16_1/8_1/16_1/4': {
          descriptions: ['stem,head|hline one,hline two|w1o5@hline one,stem,head|w1o5@hline one|hline one,hline two,stem,head', 'stem,head'],
          rhymePattern: '1202,1'
        },
        '1/8_1/4_1/8': {
          descriptions: ['stem,head|flag', 'stem,head', 'stem,head|flag'],
          rhymePattern: '12,02'
        },
        '1/8_1/4_1/8_1/4': {
          descriptions: ['stem,head|flag', 'stem,head', 'stem,head|flag', 'stem,head'],
          rhymePattern: '12,02,1'
        },
        '3/32_1/32_1/16_1/16': {
          descriptions: ['stem,head|hline one,hline two,dot|w1o2@stem,head,hline one,hline two,hline three|w1o5@stem,head,hline one, hline two|w1o5@stem,head,hline one, hline two'],
          rhymePattern: '10022020'
        },
        '3/32_1/32_1/16_1/16_1/4': {
          descriptions: ['stem,head|hline one,hline two,dot|w1o2@stem,head,hline one,hline two,hline three|w1o5@stem,head,hline one, hline two|w1o5@stem,head,hline one, hline two', 'stem,head'],
          rhymePattern: '10022020,1'
        },
        '3/8_1/16_1/16': {
          descriptions: ['stem,head|dot', 'stem,head|w1o5@hline one,hline two,stem,head'],
          rhymePattern: '1,0022'
        },
        '3/8_1/16_1/16_1/4': {
          descriptions: ['stem,head|dot', 'stem,head|w1o5@hline one,hline two,stem,head', 'stem,head'],
          rhymePattern: '1,0022,1'
        },
        '1/16_1/16_3/8': {
          descriptions: ['stem,head|w1o5@hline one,hline two,stem,head', 'stem,head|dot'],
          rhymePattern: '1220,0'
        },
        '1/16_1/16_3/8_1/4': {
          descriptions: ['stem,head|w1o5@hline one,hline two,stem,head', 'stem,head|dot', 'stem,head'],
          rhymePattern: '1220,0,1'
        },
        '1/8': {
          descriptions: ['stem,head|flag'],
          rhymePattern: '1'
        }
      },
      rhymePatternLayout: [
        ['1/4', '1/8_1/8'],
        ['1/16_1/16_1/16_1/16', '1/16_1/16_1/16_1/16_1/4', '3/32_1/32_1/16_1/16', '3/32_1/32_1/16_1/16_1/4'],
        ['1/12_1/12_1/12', '1/12_1/12_1/12_1/4', '1/20_1/20_1/20_1/20_1/20', '1/20_1/20_1/20_1/20_1/20_1/4'],
        ['3/16_1/16', '3/16_1/16_1/4', '1/16_3/16', '1/16_3/16_1/4'],
        ['1/16_1/16_1/8', '1/16_1/16_1/8_1/4', '1/8_1/16_1/16', '1/8_1/16_1/16_1/4'],
        ['1/16_1/8_1/16', '1/16_1/8_1/16_1/4', '1/8_1/4_1/8', '1/8_1/4_1/8_1/4'],
        ['3/8_1/16_1/16', '3/8_1/16_1/16_1/4', '1/16_1/16_3/8', '1/16_1/16_3/8_1/4']
      ]
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
.rp-row {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-around;
  align-items: flex-start;
  align-content: flex-start;
  width: 100%;
  height: 50px;
  border: 1px 0 0 0;
  border-top: 1px solid red;
}
.rp-col {
  flex-grow: 1;
  flex-shrink: 1;
  display: block;
  border: 0 1px 0 0;
  border-right: 1px solid red;
  padding-top: 15px;
  padding-bottom: 15px;
  height: calc(100% - 30pxd w);
}
.rp-col:last-child {
  border-right: 0;
}
</style>
