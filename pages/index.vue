<template>
  <div class="app">
    <div class="app__block" :class="{active: card.select}" v-dragged="onDragged" @click="selectCard(card)" v-for="card of cards">
      <h2 class="app__block-title">{{ card.title }}</h2>
      <h2 class="app__block-subtitle">{{ card.subtitle }}</h2>
    </div>
    <div class="app__block-big" v-if="succcessShow">
      <h2 class="app__block-title" v-for="card of newCard">{{ card }}</h2>
    </div>
    <button class="success" @click="successCard">Соеденить</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cards: [
        {
          id: 0,
          title: 'Card-1',
          subtitle: 'Text-2',
          select: false
        },
        {
          id: 1,
          title: 'Card-2',
          subtitle: 'Text-2',
          select: false,
        },
        {
          id: 2,
          title: 'Card-3',
          subtitle: 'Text-2',
          select: false
        },
      ],
      newCard: [],
      dragged: true,
      success: false,
      succcessShow: false,
    }
  },
  methods: {
    successCard() {
      this.success = true
      this.succcessShow = true
      for (let i = 0; i < this.cards.length; i++) {
        this.cards = this.cards.filter(item => item.select === false)
      }
      this.success = false
    },
    selectCard(card) {
      card.select = true
        if (this.success) {
          this.cards = this.cards.filter(item => item.title !== card.title)
        }
      this.newCard.push(card.title)
    },
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
.app__block-big {
  width: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  background: #ccc;
  box-shadow: 10px 10px 20px #000;
  cursor: pointer;
  position: relative;
}
.active {
  background: black;
  color: white;
}
.success {
  width: 140px;
  height: 50px;
  background: #00b67a;
  color: #fff;
  position: absolute;
  bottom: 30px;
  right: 30px;
  z-index: 10;
  border: none;
  outline: none;
  cursor: pointer;
}

</style>
