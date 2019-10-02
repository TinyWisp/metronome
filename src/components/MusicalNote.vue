<template>
  <div :class="['note', draw.noteClass]" :style="cssProps">
    <div :class="['piece', piece.class]" v-for="(piece, i) in draw.pieces" :key=i>
      <div :class="[part]" v-for="(part, j) in piece.parts" :key=j></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MusicalNote',
  props: {
    description: {
      type: String,
      default: ''
    },
    color: {
      type: String,
      default: 'black'
    },
    backgroundColor: {
      type: String,
      default: 'white'
    }
  },
  computed: {
    cssProps() {
      return {
        '--color': this.color,
        '--backgroundColor': this.backgroundColor
      }
    },
    draw() {
      console.log('description: ' + this.description + '\n');
      let desc = this.description;
      let noteClass = '';
      let pieces = [];

      if (desc.indexOf('>') === -1) {
        desc = '>' + desc;
      }
      let tmps = desc.split('>');
      noteClass = tmps[0];
      let piecesStr = tmps[1];

      console.log('piecesStr: ' + piecesStr + '\n');

      let pieceStrArr = piecesStr.split('|');
      for (let pieceStr of pieceStrArr) {
        if (pieceStr.indexOf('@') === -1) {
          pieceStr = '@' + pieceStr;
        }
        tmps = pieceStr.split('@');
        pieces.push({
          class: tmps[0],
          parts: tmps[1].split(',')
        });
      }

      return {
        noteClass: noteClass,
        pieces: pieces
      }
    }
  }
}
</script>

<style scoped>
.note {
  display: inline-flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: flex-start;
  align-items: flex-start;
  align-content: flex-start;
  vertical-align: top;
  width: auto;
  height: auto;
  padding: 0;
  margin-right: 10px;
}
.piece {
  width: 10px;
  height: 20px;
  display: block;
  border: 0;
  margin: 0;
  padding: 0;
  z-index: 3;
  position: relative;
}
.piece.w0o8 {
  width: 8px;
}
.piece.w0o5 {
  width: 5px;
}
.piece.w1o3 {
  width: 13px;
}
.piece.w1o5 {
  width: 15px;
}
.piece.w2 {
  width: 20px;
}
.stem {
  display: block;
  width: 1px;
  height: 100%;
  border: 0;
  margin: 0;
  padding: 0;
  position: absolute;
  right: 0;
  top: 0;
  background-color: var(--color);
}
.head {
  width: 10px;
  background: var(--color);
  border-radius: 200%;
  height: 6px;
  position: absolute;
  bottom: -6px;
  right: -1px;
  transform: rotate(-30deg);
}
.head.hollow::before {
  content: '';
  display: block;
  width: 7px;
  background: var(--backgroundColor);
  border-radius: 200%;
  position: absolute;
  height: 2px;
  bottom: 2px;
  right: 2px;
}
.flag {
  width: 10px;
  height: 18px;
  overflow: hidden;
  border: 0;
  display: block;
  position: relative;
}
.flag::before {
  content: '';
  display: block;
  width: 18px;
  height: 18px;
  border-radius: 50%;
  transform: scale(1, 1);
  position: absolute;
  left: -13px;
  top: 6px;
  border: 0;
  background-color: var(--backgroundColor);
  z-index: 5;
}
.flag::after {
  content: '';
  display: block;
  width: 18px;
  height: 18px;
  border-radius: 50%;
  transform: scale(1, 1.1);
  position: absolute;
  left: -12px;
  top: 4px;
  border: 0;
  background-color: var(--color);
  z-index: 3;
}
.hline {
  width: 100%;
  height: 3px;
  border: 0;
  background-color: var(--color);
  position: absolute;
  left: 0;
}
.hline.one {
  top: 0;
}
.hline.two {
  top: 6px;
}
.hline.three {
  top: 12px;
}
.dot {
  height: 3px;
  width: 3px;
  background-color: var(--color);
  border-radius: 50%;
  display: block;
  position: absolute;
  left: 50%;
  bottom: -3px;
}
.tuple {
  position: relative;
}
.tuple::before {
  content: '';
  display: block;
  width: calc(100% - 8px);
  height: 100px;
  border-radius: 8px;
  border-top: 1px solid var(--color);
  position: absolute;
  left: 8px;
  top: -7px;
  z-index: 1;
}
.tuple::after {
  content: '';
  position: absolute;
  font-size: 12px;
  left: calc(4px + 50% - 0.3em);
  top: calc(-7px - 0.5em);
  font-weight: bold;
  z-index: 2;
  background-color: var(--backgroundColor);
}
.tuple.t3::after {
  content: '3';
}
.tuple.t5::after {
  content: '5';
}
.tuple.t6::after {
  content: '6';
}
.empty {
}
</style>
