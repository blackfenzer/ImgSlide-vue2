<template>
  <div class="metamedia-slide-image" :style="{ width: width, height: height }">
    <ul>
      <transition name="slide" mode="out-in">
        <li
          :key="currentIndex"
          v-on:mouseover="isHover = true"
          v-on:mouseleave="isHover = false"
        >
          <div
            :style="{
              backgroundImage: `url('${imageUrls[currentIndex].url}')`,
              width: width,
              height: height,
              backgroundSize: bgSize,
              backgroundRepeat: repeat,
              cursor: checkAction(imageUrls[currentIndex].action) ? 'pointer' : 'default'
            }"
            @click="handleAction(imageUrls[currentIndex].action)"
          ></div>
        </li>
      </transition>
    </ul>
    <div class="metamedia-controls-bar-three-dot">
      <div class="metamedia-navigation-bar-three-dot">
        <span
          v-for="(url, index) in imageUrls"
          :key="index"
          @click="goToSlide(index), delayInterval()"
          :class="{ active: currentIndex === index }"
        ></span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'ImgSlide',
  props: {
    imageUrls: {
      type: Array,
      required: true,
      validator: (value) => {
        return value.every(
          (image) =>
            typeof image.url === 'string' && typeof image.action === 'object'
        )
      }
    },
    width: {
      type: [Number, String],
      default: '300px'
    },
    height: {
      type: [Number, String],
      default: '300px'
    },
    tim: {
      type: Number,
      default: 3000
    },
    bgSize: {
      type: String,
      default: 'cover'
    },
    repeat: {
      type: String,
      default: 'none'
    }
  },
  data () {
    return {
      currentIndex: 0,
      intervalId: null,
      isHover: false
    }
  },
  mounted () {
    this.startInterval()
  },
  beforeDestroy () {
    clearInterval(this.intervalId)
  },
  methods: {
    prevSlide () {
      if (this.currentIndex > 0) {
        this.currentIndex--
      } else {
        this.currentIndex = this.imageUrls.length - 1
      }
    },
    nextSlide () {
      if (this.currentIndex < this.imageUrls.length - 1) {
        this.currentIndex++
      } else {
        this.currentIndex = 0
      }
    },
    goToSlide (index) {
      this.currentIndex = index
    },
    startInterval () {
      this.intervalId = setInterval(() => {
        if (!this.isHover) {
          this.nextSlide()
        }
      }, this.tim)
    },
    delayInterval () {
      clearInterval(this.intervalId)
      this.intervalId = 0
      setTimeout(() => {
        if (!this.intervalId) {
          this.startInterval()
          console.log('start new interval')
        }
        // this.startInterval()
      }, 5000)
    },
    handleAction (act) {
      if (typeof act === 'object') {
        if (act.type === 'link') {
          window.open(act.url, '_blank')
        } else if (act.type === 'function') {
          act.handler()
        } else {
          console.log('invalid action')
        }
      }
    },
    checkAction (act) {
      if (typeof act === 'object') {
        if (act.type === 'link') {
          return true
        } else if (act.type === 'function') {
          return true
        } else {
          return false
        }
      }
      return false
    }
  }
}
</script>
<style scoped>
.metamedia-slide-image {
  position: relative;
}
.metamedia-slide-image ul {
  list-style: none;
  padding: 0;
  margin: 0;
  position: relative;
  height: 100%;
  overflow: hidden;
}
.metamedia-slide-image li {
  width: 100%;
  height: 100%;
}
.slide-enter-from {
  transform: translateX(50%);
  opacity: 0;
}
.slide-enter-to {
  transform: translateX(0%);
  opacity: 1;
}
.slide-enter-active {
  transition: all 0.15s linear;
}
.slide-leave-from {
  transform: translateX(0%);
  opacity: 1;
}
.slide-leave-to {
  transform: translateX(-50%);
  opacity: 0;
}
.slide-leave-active {
  transition: all 0.15s linear;
}
.metamedia-controls-bar-three-dot {
  margin-top: 10px;
}
.metamedia-navigation-bar-three-dot {
  display: flex;
  justify-content: center;
}
.metamedia-navigation-bar-three-dot span {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background-color: #ccc;
  margin: 0 5px;
  cursor: pointer;
}
.metamedia-navigation-bar-three-dot span.active {
  background-color: #333;
}
</style>
