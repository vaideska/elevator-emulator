<template>
<div class="elevator">
  <transition-group name="flip-list">
    <div class="block" v-for="item in items" :key="item">
      <div class="floor"></div>
      <button class="btn" @click="shuffle(item)">Click!</button>
    </div>
    <div class="block" :key="10000">
      <div class="lift" :style="{'--floor': floor, '--duration': duration}">
        {{ status }} {{ status !== 'stop' ? 6 - floor : '' }}
      </div>
    </div>
</transition-group>
</div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      items: [1, 2, 3, 4, 5],
      gap: 0,
      duration: '0s',
      floor: 5,
      status: 'stop',
    };
  },
  methods: {
    shuffle(item) {
      const gap = this.floor - item;
      if (gap === 0) {
        this.status = 'Stop';
      } else {
        this.status = gap > 0 ? 'Up' : 'Down';
      }
      this.gap = Math.abs(gap);
      this.duration = `${this.gap}s`;
      this.floor = item;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.elevator {
  display: flex;
  flex-direction: column;
  margin: 10px;
}

.block {
  display: flex;
  align-items: center;
  position: relative;
}

.floor {
  width: 75px;
  height: calc(95vh/5);
  border: 1px solid grey;
}

.lift {
  background-color: teal;
  width: 75px;
  height: calc(100vh/5);
  --floor: 5;
  bottom: calc(95vh - 95vh/5 * var(--floor));
  transition: bottom var(--duration) linear;
  position: absolute;
}

.btn {
  margin-left: 10px;
  height: 30px;
  top: auto;
  bottom: auto;
}

</style>
