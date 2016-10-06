<template>
  <div id="app">
    <div class="mask"></div>
    <div class="stage opening" :class="{active: now_view == 'opening'}">
      <div id="whiteCat"></div>
      <button class="btn_opening" @click="goToGameInfo" v-if="opening_over">繼續</button>
    </div>
    <div class="stage stage1" :class="{active: now_view == 'stage1'}"> 
      <div class="box__amanda">
        <img class="img_amanda" src="./assets/amanda.png" alt="">
      </div>
      <span>你們的好朋友<span class="span__name">阿麵咑</span>已經被公司的叛徒綁架了。</span>

      <div class="box__password">
        <input v-model="game_jack" @keyup="pass_verify('jack')" :class="game_jack_done ? 'right' : 'err' " type="" name="" maxlength="2">
        <span>-</span>
        <input v-model="game_chelsea" @keyup="pass_verify('chelsea')" :class="game_chelsea_done ? 'right' : 'err' " type="" name="" maxlength="2">
        <span>-</span>
        <input v-model="game_gore" :class="game_gore_done ? 'right' : 'err' " @keyup="pass_verify('gore')" type="" name="" maxlength="2">
        <span>-</span>
        <input v-model="game_jing" @keyup="pass_verify('jing')" :class="game_jing_done ? 'right' : 'err' " type="" name="" maxlength="2">
        <span>-</span>
        <input v-model="game_frank" @keyup="pass_verify('frank')" :class="game_frank_done ? 'right' : 'err' " name="" maxlength="2">
      </div>

    </div>
    


  </div>
</template>

<script>

var theaterJS = require("theaterjs");
var theater = theaterJS({
  "minSpeed": {
    "erase": 50,
    "type": 80
  },

  "maxSpeed": {
    "erase": 80,
    "type": 450
  }
})
theater
  .on('type:start, erase:start', function () {
    // add a class to actor's dom element when he starts typing/erasing
    var actor = theater.getCurrentActor()
    actor.$element.classList.add('is-typing')
  })
  .on('type:end, erase:end', function () {
    // and then remove it when he's done
    var actor = theater.getCurrentActor()
    actor.$element.classList.remove('is-typing')
  })


export default {
  mounted(){
    var that = this;
    theater
      .addActor('whiteCat')

    theater
        .addScene('whiteCat:噓！別出聲...', 400)
        // .addScene(1000)
        // .addScene('whiteCat:我是有正義感的白帽駭客。', 200)
        // .addScene(1000)
        // .addScene('whiteCat:這間公司裡頭有著背叛者，',1000,'你們是我唯一確定清白的人。', 400)
        // .addScene(1000)
        // .addScene('whiteCat:沒錯就是你們，',1000,'踢踢那',300,'&',300,'蘿蔔坑', 400)
        // .addScene(1000)
        // .addScene('whiteCat:現在別出聲，慢慢站起來確認彼此的存在。', 400)
        // .addScene(1000)
        .addScene(function() {
          that.opening_over = true;
        })

  },
  data () {
    return {
      now_view: 'stage1',
      opening_over: false,

      game_jack: undefined,
      game_jack_done: false,

      game_chelsea: undefined,
      game_chelsea_done: false,

      game_gore: undefined,
      game_gore_done: false,

      game_jing: undefined,
      game_jing_done: false,

      game_frank: undefined,
      game_frank_done: false,

      right_pass:{
        jack: 11,
        chelsea: 22,
        gore: 33,
        jing: 44,
        frank: 55
      }

    }
  },
  computed:{
    
  },
  methods: {
    pass_verify(who){
      console.log(this[`game_${who}`])
      if(this.right_pass[who]==this[`game_${who}`]){
        this[`game_${who}_done`] = true;
      }
    },
    goToGameInfo(){
      this.now_view = 'stage1';
    }
  }
}
</script>

<style lang="sass" scoped>
  @import url('./style.scss');
 
</style>
