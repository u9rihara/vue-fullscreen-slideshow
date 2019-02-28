<template>
  <div class="slides">
    <ul v-if="images.length">
      <li v-for="(image, index) in images" :key="image.src" :class="index === active? 'active' : ''">
        <img :src="image.src">
      </li>
    </ul>
  </div>
</template>

<script>
  require('dotenv').config();
  const axios = require('axios');
  module.exports = {
    data: () => {
      return {
        images: [],
        active: 0,
        interval: 10000
      }
    },
    created: function () {
      this.init();
    },
    methods: {
      init: function () {
        axios.get(process.env.IMAGES_JSON_URL).then(res => {
          this.images = res.data;
          if (this.images.length <= 1) {
            return;
          }
          setInterval(this.moveActive, this.interval);
        });
      },
      moveActive: function () {
        this.active++;
        if (this.active === this.images.length) {
          this.active = 0;
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
  .slides {
    width: 100%;
    height: 100%;
    ul, li, img {
      width: 100%;
      height: 100%;
    }
    ul {
      position: relative;
      margin: 0;
      padding: 0;
      list-style: none;
    }
    li {
      display: block;
      position: absolute;
      left: 0;
      top: 0;
      opacity: 0;
      transition: opacity 3s;
      &.active {
        opacity: 1;
      }
    }
    img {
      object-fit: cover;
      vertical-align: middle;
    }
  }
</style>
