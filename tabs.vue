<template>
  <div>
    <nav>
      <ul>
        <li v-for="item,i in items" v-on:click="switchItem(i)" :class="{active: i==current}" :style="{backgroundColor: item.props.color}">
        {{ item.props.name }}
        </li>
      </ul>
    </nav>
    <main>
      <div class="imgbox">
    <img :src="currentImage" />
      </div>
      <p class="category">{{ currentItem.props.title }}</p>
      <p class="name"> {{ currentItem.props.description }}</p>
      <p class="movie"> {{ currentItem.props.text }}</p>
    </main>
    
  </div> 
</template>

<script>
  module.exports = {
    data: function data() {
      return {
        current: 0,
        size: null
      }
    },
    props: ['items'],
    computed: {
      currentItem: function currentItem() {
        return this.items[this.current]
      },
      currentImageSize: function currentImageSize() {
        return 'image'
      },
      currentImage: function currentImage() {
        return 'assets/' + this.currentItem[this.currentImageSize]
      }
    },
    mounted: function mounted() {
      this.resize()
      window.onresize = this.resize
    },
    methods: {
      resize: function resize() {
        this.size = this.$el.getBoundingClientRect()
      },
      switchItem: function switchItem(i) {
        this.current = i
      }
    }
  }
</script>