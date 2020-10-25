<template>
  <div
    class="death-counter flex items-center justify-center text-white bg-red-700 text-6xl h-screen lg:h-auto"
  >
    <strong>
      <a
        id="death-counter-animate"
        href="https://covidtracking.com/"
        aria-label="COVID Tracking Project"
      ></a>
    </strong>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'
import Axios from 'axios'
import { CountUp } from 'countup.js'

@Component
export default class Counter extends Vue {
  // data
  private dailyCount: number = 0
  // Props
  @Prop({ required: true, type: Number, default: 0 }) start!: number
  @Prop({ required: true, type: Number, default: 0 }) stop!: number
  @Prop({ required: true, type: Number, default: 0 }) duration!: number

  // Methods
  public initCount(stop: number): void {
    let options = { startVal: this.start || 0, duration: this.duration || 60 }
    let countUp = new CountUp('death-counter-animate', stop, options)
    if (!countUp.error) {
      countUp.start()
    } else {
      console.error(countUp.error)
    }
  }
  // Lifecycle hook
  mounted() {
    Axios.get('https://api.covidtracking.com/v1/us/current.json').then(
      (response) => {
        if (response.status === 200) {
          this.dailyCount = response.data[0].death
        } else {
          this.dailyCount = this.stop
        }
        this.initCount(this.dailyCount)
      }
    )
  }
}
</script>

<style>
@keyframes curtain {
  from {
    transform: translate3d(0, 0, 0);
  }

  to {
    transform: translate3d(100%, 0, 0);
  }
}
@supports (animation: 600ms 1200ms forwards normal curtain) {
  .death-counter {
      position: relative;
      overflow: hidden;
  }
  .death-counter:after {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: white;
      animation: 1s 1s forwards normal curtain;
      transform: translate3d(0, 0, 0);
  }
}
.death-counter {
    grid-row: 1;
}
</style>
