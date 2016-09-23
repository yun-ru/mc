<template>
  <div id="app">
    <div v-show="showMenu" class="menu">
      <div class="closeBtn" @click="toggleMenu">&times;</div>
      <select v-model="selectedItem" @change="init">
        <option v-for="item in items" :value="item.imgSrc">{{item.title}}</option>
      </select>
    </div>
    <div class="btns">
      <div class="menuBtn" @click="toggleMenu"></div>
      <div class="countDownBtn" @click="countingDown">
        <div v-show="counting" class="count">
          01 : {{time}}
        </div>
      </div>
    </div>
    <div class="main">
      <img :src="selectedItem">
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      time: 59,
      showMenu: false,
      counting: false,
      selectedItem: '/static/images/pm_02.png',
      items: [
        {id: 1, title: '買飲料送勁辣雞腿堡', imgSrc: '/static/images/pm_01.png'},
        {id: 2, title: '買飲料送大麥克', imgSrc: '/static/images/pm_02.png'},
        {id: 3, title: '買套餐送辣雞翅', imgSrc: '/static/images/pm_03.png'},
        {id: 4, title: '買套餐送雞塊', imgSrc: '/static/images/pm_04.png'},
        {id: 5, title: '一元咖啡', imgSrc: '/static/images/am_03.png'},
        {id: 6, title: '買有氧早餐送火腿蛋堡', imgSrc: '/static/images/am_04.png'},
        {id: 7, title: '冰炫風買一送一', imgSrc: '/static/images/snack_01.png'},
        {id: 8, title: '大薯買一送一', imgSrc: '/static/images/pm_06.png'},
        {id: 9, title: '買套餐送聖代', imgSrc: '/static/images/pm_07.png'}
      ]
    }
  },
  methods: {
    init () {
      clearInterval(this.interval)
      this.counting = false
      this.showMenu = false
      this.interval = null
      this.time = 59
    },
    toggleMenu () {
      this.showMenu = !this.showMenu
    },
    countingDown () {
      this.counting = true
      if (this.interval) {
        clearInterval(this.interval)
        this.interval = null
      } else {
        this.interval = setInterval(function () {
          if (this.time > 50) {
            this.time -= 1
          } else {
            this.time = 59
          }
        }.bind(this), 1000)
      }
    }
  }
}
</script>

<style lang="stylus">
  html,body,div,img
    padding: 0
    margin: 0
    box-sizing: border-box
  html,body
    background-color: #fff
  .menu
    position: absolute
    z-index: 2
    background-color: rgba(#000,0.3)
    width: 100%
    height: 100%
    text-align: center
    .closeBtn
      color: #fff
      text-align: right
      padding: 15px
      font-size: 20px
    select
      font-size: 25px
      margin-top: 20px
  .btns
    position: absolute
    z-index: 1
    width: 100%
    height: 100%
    .menuBtn
      width: 100%
      height: 50px
    .countDownBtn
      position: absolute
      bottom: 0
      height: 63px
      width: 100%
      .count
        background-image: url('assets/countdown-bg.png')
        background-color: #f5aa0a
        background-size: 100%
        background-repeat: no-repeat
        background-position: center center
        color: #fff
        text-align: right
        padding-top: 22px
        padding-right: 65px
        font-size: 21px
        height: 100%
  .main
    position: absolute
    width: 100%
    overflow: hidden
    img
      width: 100%
      margin-top: -20px
      float: left

</style>
