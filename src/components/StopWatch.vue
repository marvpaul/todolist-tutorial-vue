<template>
  <article class="stopwatch">
    <div class="display">{{ display }}</div>
    <div class="buttons">
      <button @click="startStop">{{ isRunning ? "Stop" : "Start" }}</button>
      <button @click="reset">Reset</button>
    </div>
  </article>
</template>

<script>
export default {
  name: "StopWatch",
  data() {
    return {
      isRunning: false,
      milliseconds: 0,
      seconds: 0,
      minutes: 0,
      hours: 0,
      timer: null,
    };
  },
  mounted(){
    if(this.start){
      this.startStop();
    }
  },
  props: {
    start: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    display() {
      return (
        this.formatTime(this.hours) +
        ":" +
        this.formatTime(this.minutes) +
        ":" +
        this.formatTime(this.seconds) +
        ":" +
        this.formatTime(this.milliseconds)
      );
    },
  },
  methods: {
    startStop() {
      if (!this.isRunning) {
        this.timer = setInterval(this.updateTime, 33);
      } else {
        clearInterval(this.timer);
      }
      this.isRunning = !this.isRunning;
    },
    reset() {
      clearInterval(this.timer);
      this.milliseconds = 0;
      this.seconds = 0;
      this.minutes = 0;
      this.hours = 0;
      this.isRunning = false;
    },
    updateTime() {
      this.milliseconds += 33;
      if (this.milliseconds >= 1000) {
        this.seconds++;
        this.milliseconds -= 1000;
        if (this.seconds === 60) {
          this.seconds = 0;
          this.minutes++;
          if (this.minutes === 60) {
            this.minutes = 0;
            this.hours++;
          }
        }
      }
    },
    formatTime(time) {
      return time < 10 ? "0" + time : time;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.stopwatch{
  width: 60%;
}

.stopwatch .display{
  font-size: 2rem;
  font-weight: bold;
  padding: 10px; 
  border: 2px solid #333;
  border-radius: 10px;
  background-color: #f8f8f8;
  margin-bottom: 20px;
}

.stopwatch .buttons {
  display: flex;
  justify-content: space-around;
}

</style>
