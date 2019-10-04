<template>
  <div id="app">
    <div class="metronome-container">
      <div class="btn btn-start" v-if="!started" @click="start()"></div>
      <div class="btn btn-stop" v-if="started" @click="stop()"></div>
      <Metronome :bpm="bpm" :rhymePattern="rhymePattern" class="metronome" ref="metronome"></Metronome>
    </div>
    <div class="row">
      <div class="col bpm-control">
        <em class="btn btn-left" @click="modifyBpm(-10)">-</em>
        <em class="btn btn-left" @click="modifyBpm(-1)">-</em>
         {{bpm}}
        <em class="btn btn-right" @click="modifyBpm(1)">+</em>
        <em class="btn btn-right" @click="modifyBpm(10)">+</em>
      </div>
    </div>
    <div class="row" :key=i v-for="(row, i) in rhymePatternRows">
      <div
        :class="{'col': true, 'col-rp-selected': notes[rp]['rhymePattern'] == rhymePattern}"
        :style="{width: 100 / row.length + '%'}"
        :key=j v-for="(rp, j) in row">
        <div class="musical-note-container" @click="setRhymePattern(notes[rp]['rhymePattern'])">
          <MusicalNote
            color="#cccccc"
            backgroundColor="#333333"
            class="musical-note"
            :description="description"
            :key=k
            v-for="(description, k) in notes[rp]['descriptions']">
          </MusicalNote>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Metronome from './components/Metronome.vue'
import MusicalNote from './components/MusicalNote.vue'

export default {
  name: 'app',
  components: {
    Metronome,
    MusicalNote
  },
  data() {
    return {
      bpm: 60,
      rhymePattern: '1',
      started: false,
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
          rhymePattern: '1222,1'
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
          descriptions: ['tuple t5>stem,head|w1o3@hline one,stem,head|w1o3@hline one,stem,head|w1o3@hline one,stem,head|w1o3@hline one,stem,head', 'stem,head'],
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
          descriptions: ['stem,head|flag|stem,head|empty|stem,head|flag'],
          rhymePattern: '12,02'
        },
        '1/8_1/4_1/8_1/4': {
          descriptions: ['stem,head|flag|stem,head|empty|stem,head|flag|stem,head'],
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
      rhymePatternRows: [
        ['1/4', '1/8_1/8'],
        ['1/16_1/16_1/16_1/16', '1/16_1/16_1/16_1/16_1/4', '3/32_1/32_1/16_1/16', '3/32_1/32_1/16_1/16_1/4'],
        ['1/12_1/12_1/12', '1/12_1/12_1/12_1/4', '1/20_1/20_1/20_1/20_1/20', '1/20_1/20_1/20_1/20_1/20_1/4'],
        ['3/16_1/16', '3/16_1/16_1/4', '1/16_3/16', '1/16_3/16_1/4'],
        ['1/16_1/16_1/8', '1/16_1/16_1/8_1/4', '1/8_1/16_1/16', '1/8_1/16_1/16_1/4'],
        ['1/16_1/8_1/16', '1/16_1/8_1/16_1/4', '1/8_1/4_1/8', '1/8_1/4_1/8_1/4'],
        ['3/8_1/16_1/16', '3/8_1/16_1/16_1/4', '1/16_1/16_3/8', '1/16_1/16_3/8_1/4']
      ]
    }
  },
  methods: {
    modifyBpm(val) {
      this.bpm = this.bpm + val;
      this.stop();
    },
    setRhymePattern(rhymePattern) {
      this.rhymePattern = rhymePattern;
    },
    start() {
      this.started = true;
      this.$refs.metronome.start();
    },
    stop() {
      this.started = false;
      this.$refs.metronome.stop();
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
  background-color: #333333;
}
.metronome-container {
  width: 100%;
  height: 150px;
  overflow: hidden;
  border: 1px solid red;
  position: relative;
}
.metronome-container .btn {
  display: block;
  position: absolute;
  left: calc(50% - 16px);
  bottom: 10px;
  border-color: #cccccc;
  z-index: 11;
}
.metronome-container .btn-start {
  border-top: 16px solid transparent;
  border-left: 32px solid #cccccc;
  border-bottom: 16px solid transparent;
  border-right: 0;
  width: 0;
  height: 0;
}
.metronome-container .btn-stop {
  border-left: 8px solid #cccccc;
  border-right: 8px solid #cccccc;
  border-top: 0;
  border-bottom: 0;
  width: 16px;
  height: 32px;
}
.metronome-container .metronome {
  z-index: 10;
}
.row {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-around;
  align-items: flex-start;
  align-content: flex-start;
  width: 100%;
  height: 50px;
  border: 0;
}
.col {
  flex-grow: 1;
  flex-shrink: 1;
  display: block;
  border: 0 1px 0 0;
  border-right: 1px solid #cccccc;
  border-top: 1px solid #cccccc;
  padding: 0;
  margin: 0;
  height: calc(100% - 1px);
  overflow: hidden;
}
.col:last-child {
  border-right: 0;
}
.col-rp-selected {
  box-shadow: 0 0 5px white;
}
.musical-note-container {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
  width: calc(100% -  20px);
  height: calc(100% - 30px);
  margin: 15px auto;
}
.musical-note:last-child {
  margin-right: 0;
}
.musical-note {
  flex-shrink: 1;
  flex-grow: 0;
  margin-right: 10px;
}
.bpm-control {
  font-size: 32px;
  line-height: 50px;
  color: #cccccc;
}
.bpm-control .btn {
  display: inline-block;
  width: 32px;
  height: 32px;
  border: 1px solid #cccccc;
  border-radius: 50%;
  color: #cccccc;
  font-size: 32px;
  line-height: 32px;
  background-color: #333333;
}
.bpm-control .btn-left {
  margin-right: 10px;
}
.bpm-control .btn-right {
  margin-left: 10px;
}
</style>
