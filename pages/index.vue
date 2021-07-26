<template>
  <div class="app">
    <div class="app__block" v-dragged="onDragged">
      <h2 class="app__block-title">Text-1</h2>
      <h2 class="app__block-subtitle">Text-2</h2>
    </div>
    <div class="app__block" v-dragged="onDragged">
      <h2 class="app__block-title">Text-1</h2>
      <h2 class="app__block-subtitle">Text-2</h2>
    </div>
    <div class="app__block" v-dragged="onDragged">
      <h2 class="app__block-title">Text-1</h2>
      <h2 class="app__block-subtitle">Text-2</h2>
    </div>
    <div class="app__block" v-dragged="onDragged">
      <h2 class="app__block-title">Text-1</h2>
      <h2 class="app__block-subtitle">Text-2</h2>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dragged: true,
    }
  },
  methods: {
    onDragged({ el, deltaX, deltaY, offsetX, offsetY, clientX, clientY, first, last }) {
      if (first) {
        this.dragged = true
        return
      }
      if (last) {
        this.dragged = false
        return
      }
      let l = +window.getComputedStyle(el)['left'].slice(0, -2) || 0
      let t = +window.getComputedStyle(el)['top'].slice(0, -2) || 0
      el.style.left = l + deltaX + 'px'
      el.style.top = t + deltaY + 'px'
    }
  }
}
</script>
<style>
.app {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.app__block {
  width: 200px;
  height: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  background: #ccc;
  box-shadow: 10px 10px 20px #000;
  cursor: pointer;
  position: relative;
}
</style>
