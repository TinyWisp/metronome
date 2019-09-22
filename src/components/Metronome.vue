<template>
  <div class="metronome" ref="metronome" :style="cssProps">
    <div v-bind:class="['rotate-box', counter % 2 == 0 ? 'rotate-box-right' : 'rotate-box-left']">
      <div class="ball"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Metronome',
  props: {
    bpm: {
      type: Number,
      default: 40
    },
    rhymePattern: {
      type: String,
      default: '1'
    }
  },
  computed: {
    period() {
      return Math.floor(60 * 1000 / this.bpm);
    },
    beats() {
      let beats = [];

      let notes = this.rhymePattern.split(',');
      for (let note of notes) {
        let beat = [];

        let length = note.length;
        for (let j=0; j<length; j++) {
          let char = note.charAt(j);
          if (char !== '0') {
            beat.push({
              time: this.period * j / length,
              type: char
            });
          }
        }

        beats.push(beat);
      }

      return beats;
    },
    cssProps() {
      return {
        '--motion-angle': this.rbAngle + 'rad',
        '--ball-radius': '20px',
        '--ball-period': this.period + 'ms',
        '--rotate-box-height': this.rbHeight + 'px'
      }
    }
  },
  data() {
    return {
        rbHeight: 0,
        rbAngle: '0rad',

        started: false,
        timer : null,
        counter : 0,

        audioCtx: null,
        gain: null,
        beepFrequency: {
          '1': 1000,
          '2': 440
        }
    }
  },
  methods: {
    beep(type) {
      let oscillator = this.audioCtx.createOscillator();
      oscillator.connect(this.gain);
      oscillator.frequency.value = this.beepFrequency[type];
      oscillator.type = "sine";
      oscillator.start(0);
      oscillator.stop(this.audioCtx.currentTime + 0.008);
    },
    start() {
      this.started = true;
      this.timer = setInterval(function(){
        this.rotate = this.counter % 2 == 0
          ? this.angle
          : 0;

        let which = this.counter % this.beats.length;
        for (let beat of this.beats[which]) {
          setTimeout(function(){
            this.beep(beat.type);
          }.bind(this), beat.time)
        }

        this.counter = this.counter + 1;
      }.bind(this), this.period);
    },
    stop() {
      this.started = false;
      this.counter = 0;
      clearInterval(this.timer);
    }
  },
  mounted() {
    let mwidth = this.$refs.metronome.clientWidth;
    let mheight = this.$refs.metronome.clientHeight;

    let motionRadius = (mwidth * mwidth + 4 * mheight * mheight) / (8 * mheight);
    this.rbAngle = 2 * Math.asin(mwidth / (2 * motionRadius));
    this.rbHeight = 2 * Math.sqrt(motionRadius * motionRadius - (mwidth / 2) * (mwidth / 2));

    this.audioCtx = new AudioContext();
    this.gain = this.audioCtx.createGain();
    this.gain.connect(this.audioCtx.destination);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.metronome {
  width: calc(100% - var(--ball-radius) * 2);
  height: calc(100% - var(--ball-radius) * 2);
  margin: var(--ball-radius);
  padding: 0;
  border: 0;
  position: relative;
}
.rotate-box {
  position: absolute;
  margin: 0;
  padding: 0;
  border: 1px solid blue;
  transition-property: transform;
  transition-timing-function: linear;
  transition-duration: var(--ball-period);
  width: 100%;
  height: var(--rotate-box-height);
  left: 0;
  top: 100%;
}
.rotate-box-right {
  transform: rotate(var(--motion-angle));
}
.rotate-box-left {
  transform: rotate(0deg);
}
.ball {
  width: 0;
  height: 0;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  left: 0;
  top: 0;
}
.ball::before {
  content: '';
  flex: none;
  width: calc(var(--ball-radius) * 2);
  height: calc(var(--ball-radius) * 2);
	display: block;
	margin: 0;
  padding: 0;
	border-radius: 50%;
  background-color: rgb(49, 145, 231);
	box-shadow: inset -25px -15px 40px rgba(0,0,0,.3);
	background-image: linear-gradient(-45deg, rgba(255,255,220,.3) 0%, transparent 100%);
}
</style>
