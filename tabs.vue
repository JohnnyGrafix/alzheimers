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
      <h3>{{ currentItem.props.title }}</h3>
	  <p id="caption"> {{ currentItem.props.caption }}</p>
	  <div class="imgntext">
	  <div class="imgbox">
	  <img :src="currentImage" />
	  </div>
	  <div class="descriptions">
      <p id="col1"> {{ currentItem.props.description }}</p>
	  <p id="col2"> {{ currentItem.props.description2}}</p>
	  <p id="col3"> {{ currentItem.props.description3}}</p>
	  </div>
	  <div class="numbers">
      <p id="n1"> {{ currentItem.props.label }}</p>
	  <p id="n2"> {{ currentItem.props.label2}}</p>
	  <p id="n3"> {{ currentItem.props.label3}}</p>
	  <p id="n4"> {{ currentItem.props.label4}}</p>
	  </div>
	  </div>
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