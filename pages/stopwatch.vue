<template>
  <section class="main">
    <div class="timer-block">
        <div class="timer">
          <p>{{ minute + ':' + second + ':' + milliseconds }}</p>
        </div>
        <div class="one-button">
          <button
            v-on:click="clearStopWatch()"
            class="button-round"
          >
            NEW ROUND
          </button>
        </div>
        <div class="two-button">
          <button 
            v-on:click="start()"
            class="button-start"
          >
            START
          </button>
          <button 
            v-on:click="stop()"
            class="button-stop"
          >
            {{ rightButton }}
          </button>
        </div>
    </div>
    <transition name="fade">
      <div 
        v-if="stopWatchHistory.length"
        class="history-block"
      >
        <button 
          v-on:click="clearHistory()"
          class="button-clear"
        >
          clear
        </button>
        <ol start="1">
          <li
            class="list"
            v-for="(time, index) in stopWatchHistory"
            :key="index"
            >{{ time }}</li>
        </ol>
      </div>
    </transition>
  </section>
</template>

<script>

export default {

  layout: 'project',

  data: () => ({
    milliseconds: 0,
    second: 0,
    minute: 0,
    timer: false,
    rightButton: 'STOP',
    stopWatchHistory: []
  }),

  methods: {
    start () {
        if (!this.timer) {
            window.intervalId = window.setInterval (() => this.milliseconds += 1, 10);
            this.timer = true;
            this.rightButton = 'STOP';
        }
    },
    stop () {
        if (this.rightButton === 'RESET') {
          this.timer = false;
          window.clearInterval(window.intervalId);
          this.milliseconds = 0;
          this.second = 0;
          this.minute = 0;
        } else {
          this.timer = false;
          window.clearInterval(window.intervalId);
          this.rightButton = 'RESET';
        }
    },
    clearStopWatch () {
      if ( this.minute + ':' + this.second + ':' + this.milliseconds !== '0:0:0') {
        this.stopWatchHistory.push(this.minute + ':' + this.second + ':' + this.milliseconds);
      }
      /*if (this.stopWatchHistory.length > 6) {
        this.stopWatchHistory.shift();
      }*/
        this.rightButton = 'STOP';
        window.clearInterval(window.intervalId);
        this.milliseconds = 0;
        this.second = 0;
        this.minute = 0;
        this.timer = false;
        window.intervalId = window.setInterval (() => this.milliseconds += 1, 10);
    },
    clearHistory () {
      this.stopWatchHistory = [];
    }
  },

  watch: {
      milliseconds: function() {
          if (this.milliseconds > 100) {
            this.second += 1;
            this.milliseconds = 0;
          }
      },
      second: function () {
          if (this.second > 59){
              this.minute += 1;
              this.second = 0;
          }
      }
  }
}
</script>


<style>
.main {
  min-height: 100vh;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.timer-block {
  width: 300px;
  height: 300px;
  border: 1px solid lightskyblue;
  border-radius: 50%;
  position: relative;
}
.history-block{
  margin-left: 550px;
  width: 150px;
  height: 300px;
  border: 1px solid lightskyblue;
  border-radius: 5%;
  overflow-x: scroll;
  position: fixed;
}
.timer {
  font-size: 40px;
  padding: 0;
  margin-top: 30px;
}
.button-stop {
  background: red;
  color: white;
  border: 0;
  border-bottom-right-radius: 100%;
  padding-left: 30px;
  text-align: left;
  width: 50%;
  outline: none;
  font-size: 22px;
  opacity: 0.6;
}
.button-clear {
 background: transparent;
  color: lightskyblue;
  border: 1px solid lightskyblue;
  width: 100%;
  outline: none;
  font-size: 22px;
  border-top-left-radius: 7px;
  border-top-right-radius: 7px;
}
.button-round {
  background: transparent;
  color: lightskyblue;
  border: 1px solid lightskyblue;
  width: 100%;
  height: 100%;
  outline: none;
  font-size: 22px;
  border-top-left-radius: 30px;
  border-top-right-radius: 30px;
}
.button-start {
  background: green;
  color: white;
  border: 0;
  border-bottom-left-radius: 100%;
  padding-right: 30px;
  text-align: right;
  width: 50%;
  margin: 0;
  outline: none;
  font-size: 22px;
  opacity: 0.6;
}
.two-button {
  display: flex;
  position: absolute;
  bottom: 0px;
  height: 145px;
  width: 100%;
}
.one-button {
  width: 100%;
  height: 50px;
  display: flex;
  position: absolute;
  bottom: 145px;
}
.list {
  font-size: 20px;
  height: 40px;
  padding: 8px;
  background: lightgray;
  border: 1px solid lightskyblue;
  opacity: 0.8;
  vertical-align: middle;
}
ul {
  padding: 0;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
</style>