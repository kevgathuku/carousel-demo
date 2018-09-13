<template>
  <div class="fish carousel">
    <div class="content" :style="{'width': `${width}px`}">
      <ul class="list"
        @click="clickHandler"
        :style="{
          width: `${width * childrenLength}px`,
          transform: `translate3d(-${activeIndex * width}px, 0px, 0px)`,
          transition: '-webkit-transform 500ms ease'
        }">
        <carousel-item v-for="index in 4" :key="index">
          <h3 class="carousel-xx" v-html="index"></h3>
        </carousel-item>
      </ul>
    </div>
    <ul class="dots">
      <li
        :style="dotStyle"
        v-for="(i, index) in childrenLength"
        :key="i"
        :class="{'active': activeIndex === index}"
        @click.stop="dotClickHandler(index)"></li>
    </ul>
  </div>
</template>

<script>
import CarouselItem from './CarouselItem';

export default {
  name: 'HelloCarousel',
  components: {
    CarouselItem,
  },
  props: {
    dotStyle: { type: String, default: '' },
  },
  data() {
    return {
      width: 0,
      childrenLength: 0,
      activeIndex: 0,
    };
  },
  mounted() {
    // each element takes up full available width
    this.width = this.$el.offsetWidth;
    this.childrenLength = this.$children.length;
    this.$children.forEach((element) => {
      const child = element;
      child.$el.style.width = `${this.width}px`;
    });
  },
  methods: {
    clickHandler() {
      if (this.activeIndex >= this.childrenLength - 1) {
        this.activeIndex = 0;
      } else {
        this.activeIndex += 1;
      }
    },
    dotClickHandler(index) {
      this.activeIndex = index;
    },
  },
};
</script>

<style>
.carousel-xx {
  height: 200px;
  line-height: 200px;
  text-align: center;
  vertical-align: middle;
  background: #506b9e;
  color: #fff;
  font-size: 2rem;
}
</style>
