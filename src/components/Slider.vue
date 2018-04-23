<template>
  <div class="vc-slider">
    <div class="vc-slider-hue-warp">
      <hue v-model="colors" @change="hueChange"></hue>
    </div>
    <div v-if="showSwatches" class="vc-slider-swatches">
      <div class="vc-slider-swatch" v-for="(offset, index) in swatches" :key="index" :data-index="index"
        @click="handleSwClick(index, offset)">
        <div class="vc-slider-swatch-picker"
        :aria-label="'color:' + 'hsl(' + colors.hsl.h + ', 50%, ' + (offset * 100) + '%)'"
        :class="{'vc-slider-swatch-picker--active': offset == activeOffset}"
        :style="{background: 'hsl(' + colors.hsl.h + ', 50%, ' + (offset * 100) + '%)'}"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
import colorMixin from '../mixin/color'
import hue from './common/Hue.vue'

export default {
  name: 'Slider',
  mixins: [colorMixin],
  props: {
    direction: String,
    showSwatches: Boolean
  },
  components: {
    hue
  },
  computed: {
    activeOffset () {
      if (Math.round(this.colors.hsl.s * 100) / 100 === 0.50) {
        return Math.round(this.colors.hsl.l * 100) / 100
      }
      return 0
    }
  },
  data () {
    return {
      swatches: ['.80', '.65', '.50', '.35', '.20']
    }
  },
  methods: {
    hueChange (data) {
      this.colorChange(data)
    },
    handleSwClick (index, offset) {
      this.colorChange({
        h: this.colors.hsl.h,
        s: 0.5,
        l: offset,
        source: 'hsl'
      })
    }
  }
}
</script>

<style>
.vc-slider {
  --vc-slider-height: 4px;
  position: relative;
  width: 410px;
}
.vc-slider-hue-warp {
  height: var(--vc-slider-height);
  position: relative;
}
.vc-slider-hue-warp .vc-hue-picker {
  width: 14px;
  height: 14px;
  border-radius: 7px;
  transform: translate(-7px, -2px);
  background-color: rgb(248, 248, 248);
  box-shadow: 0 0 0 2px white, 0 0 0 6px rgba(230, 230, 230, 1), 0 0 0 8px white;
}
.vc-hue {
  border-radius: calc(var(--vc-slider-height)/2);
}
.vc-slider-swatches {
  display: flex;
  margin-top: 20px;
}
.vc-slider-swatch {
  margin-right: 1px;
  flex: 1;
  width: 20%;
}
.vc-slider-swatch:first-child {
  margin-right: 1px;
}
.vc-slider-swatch:first-child .vc-slider-swatch-picker {
  border-radius: 2px 0px 0px 2px;
}
.vc-slider-swatch:last-child {
  margin-right: 0;
}
.vc-slider-swatch:last-child .vc-slider-swatch-picker {
  border-radius: 0px 2px 2px 0px;
}
.vc-slider-swatch-picker {
  cursor: pointer;
  height: 12px;
}
.vc-slider-swatch-picker--active {
  transform: scaleY(1.8);
  border-radius: 3.6px/2px;
}
</style>
