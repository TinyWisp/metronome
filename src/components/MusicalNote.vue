<template>
  <div :class="['note', draw.noteClass]">
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
    }
  },
  computed: {
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
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: flex-start;
  align-items: flex-start;
  align-content: flex-start;
  width: auto;
  height: auto;
  padding: 0;
}
.piece {
  width: 10px;
  height: 20px;
  display: block;
  border: 0;
  margin: 0;
  padding: 0;
  position: relative;
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
  background-color: black;
}
.head {
  width: 10px;
  background: black;
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
  width: 6px;
  background: white;
  border-radius: 200%;
  position: absolute;
  height: 2px;
  bottom: 2px;
  right: 2px;
}
.hline {
  width: 100%;
  height: 3px;
  border: 0;
  background-color: black;
  position: absolute;
  left: 0;
}
.hline.one {
  top: 0;
}
.hline.two {
  top: 6px;
}
</style>
