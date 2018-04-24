<template>
  <div id="app">
    <div class="header-container">
      <div class="header-bg" :style="{'background-color': bgc}"></div>
    </div>

    <div class="demo-container">
      <div class="demo-list">
        <div class="demo-item">
          <slider-picker v-model="colors" showSwatches="true"></slider-picker>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import slider from '../src/components/Slider.vue'

let defaultProps = {
  hex: '#40BFBF',
  hsl: {
    h: 180,
    s: 0.5,
    l: 0.5,
    a: 1
  },
  a: 1
}

export default {
  components: {
    'slider-picker': slider,
  },
  data () {
    return {
      colors: defaultProps
    }
  },
  computed: {
    bgc () {
      return this.colors.hex
    }
  },
  methods: {
    onOk () {
      console.log('ok')
    },
    onCancel () {
      console.log('cancel')
    },
    updateValue (value) {
      this.colors = value
    }
  },
  created () {
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
html {
  font-family: 'Source Sans Pro', 'Helvetica Neue', Arial, sans-serif;
}

.header-container {
  position: relative;
}
.header-bg {
  position: relative;
  top: 0;
  left: 0;
  right: 0;
  min-height: 380px;
  background-color: #333;
  z-index: 0;
}
.header {
  display: flex;
  max-width: 780px;
  margin: 0 auto;
  padding: 20px 0;
}
.intro-wrap {
  flex: 1;
  margin-right: 100px;
}
.intro {
  width: 300px;
  color: rgba(0, 0, 0, 0.65098);
}
.intro > h1 {
  font-size: 40px;
  font-weight: normal;
  line-height: 60px;
}
.intro > p {
  font-size: 16px;
  font-weight: normal;
  line-height: 22px;
}

.demo-container {
  max-width: 780px;
  margin: 2rem auto;
  position: relative;
  z-index: 2;
}
.demo-list {
  display: flex;
  margin-bottom: 20px;
}
.demo-item {
  position: relative;
  margin-bottom: 10px;
  margin: 0 10px 0 10px;
  z-index: 2;
  width: 100%;
}
.demo-item h6 {
  margin: 0;
  padding: 5px 0;
  color: #666;
}
</style>
