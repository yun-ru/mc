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
      <div class="countDownBtn" @click="showAlertBox">
        <div v-show="counting" class="count unselectable">
          01 : {{time}}
        </div>
      </div>
    </div>
    <div class="main">
      <img :src="selectedItem">
    </div>


    <div class="modal fade" tabindex="-1" role="dialog">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-body">
            <h4>確認兌換優惠</h4>
            <p>請確認您已在麥當勞餐廳櫃檯，點選「立即兌換」後，需於兩分鐘內出示給結帳人員。</p>
            <div class="text-right">
              <button type="button" class="btn btn-link" data-dismiss="modal">暫不兌換</button>
              <button type="button" class="btn btn-link" data-dismiss="modal" @click="countingDown">立即兌換</button>
            </div>
          </div>
        </div><!-- /.modal-content -->
      </div><!-- /.modal-dialog -->
    </div><!-- /.modal -->

  </div>
</template>

<script>
export default {
  data () {
    return {
      time: 59,
      showMenu: false,
      counting: false,
      selectedItem: '/static/images/pm_02.jpg',
      items: [
        {title: '一元薯餅', imgSrc: '/static/images/1001.jpg'},
        {title: '一元咖啡', imgSrc: '/static/images/1002.jpg'},
        {title: '大薯買一送一', imgSrc: '/static/images/2001.jpg'},
        {title: '冰炫風買一送一', imgSrc: '/static/images/20002.jpg'},
        {title: '聖代買一送一', imgSrc: '/static/images/2003.jpg'},
        {title: '買有氧早餐送火腿蛋堡', imgSrc: '/static/images/3001.jpg'},
        {title: '買套餐送勁辣雞腿堡', imgSrc: '/static/images/3002.jpg'},
        {title: '買套餐送大麥克', imgSrc: '/static/images/3003.jpg'},
        {title: '買套餐送辣雞翅', imgSrc: '/static/images/3004.jpg'},
        {title: '買套餐送雞塊', imgSrc: '/static/images/3005.jpg'},
        {title: '買套餐送聖代', imgSrc: '/static/images/3006.jpg'},
        {title: '買套餐送蘋果派', imgSrc: '/static/images/3007.jpg'},
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
    showAlertBox () {
      if (!this.counting){
        $(".modal").modal()
      }
    },
    countingDown () {
      if (!this.interval) {
        this.counting = true
        this.interval = setInterval(function () {
          if (this.time > 0) {
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
  countingBarH = 90px
  mcYellow = #f5aa0a
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
      height: countingBarH
      width: 100%
      .count
        background-image: url('assets/countdown-bg.png')
        background-color: mcYellow
        background-size: 100%
        background-repeat: no-repeat
        background-position: center center
        color: #fff
        text-align: right
        padding-right: 65px
        font-size: 21px
        height: countingBarH
        line-height: countingBarH
  .main
    position: absolute
    width: 100%
    overflow: hidden
    img
      width: 100%
      margin-top: -20px
      float: left

  // Modal
  .modal-dialog
    display: flex
    justify-content: center
    align-items: center
    height: 100%
    margin: 0
    .modal-content
      margin: 20px
      margin-bottom: 60px
      h4
        margin-bottom: 20px


  // Util
  .unselectable {
    -webkit-touch-callout: none
    -webkit-user-select: none
    -khtml-user-select: none
    -moz-user-select: none
    -ms-user-select: none
    user-select: none
  }

</style>
