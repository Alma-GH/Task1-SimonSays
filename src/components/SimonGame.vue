<template>
  <div class="game">

    <div class="controls">
      <StartButton :disabled="onplay" :cb="startPlay"/>
      <SelectDifficult :disabled="onplay" :change-difficult="changeDifficult"/>
    </div>


    <SimonInfo v-if="onplay" :wait="wait" :round="getNowPathLen()"/>

    <SimonBlock
        :light="light"
        :isWait="wait"
        :next="clickSimonBtn"
    />

    <div v-if="message !== null" :class="{messageStyle:true, loseMessage:!message}">
       {{message?"YOU WIN":`Sorry, you lost after ${getNowPathLen()} rounds`}}
    </div>

  </div>
</template>

<script>
import StartButton from "@/components/StartButton";
import SimonBlock from "@/components/SimonBlock"
import SelectDifficult from "@/components/SelectDifficult";
import SimonInfo from "@/components/SimonInfo";
import {allOffLight} from "@/tools/const";
import {getRandomInt} from "@/tools/utils";
import sound1 from "@/media/sounds_1.mp3"
import sound2 from "@/media/sounds_2.mp3"
import sound3 from "@/media/sounds_3.mp3"
import sound4 from "@/media/sounds_4.mp3"

export default {
  components:{
    StartButton, SimonBlock, SelectDifficult, SimonInfo
  },
  data(){
    return {
      //const(options of game)
      pathLen: 10,
      lightTime: 200,
      srcSounds: [sound1, sound2, sound3,sound4],

      //var
      roundsLeft: 10, //depends on pathLen
      path:[],
      pathCursor: 0,


      difficult: 1,
      onplay: false,


      message: null,
      wait: false,
      light: [...allOffLight]
    }
  },
  methods:{

    makeSound(sound){
      let audio = new Audio()
      audio.src = sound
      audio.play()
    },

    getDelayFromDifficult(difficult){
      switch (difficult){
        case 1:
          return 1.5
        case 2:
          return 1
        case 3:
          return 0.4
        default:
          return 1.5
      }
    },

    getNowPathLen(){
      return this.pathLen - this.roundsLeft + 1
    },

    initVars(){
      //remaining rounds
      this.roundsLeft = this.pathLen

      //path
      this.path = []

      //cursor for path
      this.pathCursor = 0
    },

    putWinLoseMessage(isLose){
      console.log(isLose)
      this.message = !isLose
      this.wait = false
      this.onplay = false
      setTimeout(()=>this.message=null, 3000)
    },

    changeDifficult(e){
      this.difficult = +e.target.value
    },

    resetGame(){
      this.initVars()

      this.onplay = false
      this.wait = false
      this.message = null
    },

    startPlay(){
      this.resetGame()
      //start game
      this.onplay = true

      //init
      let newPath = []
      for (let i = 0; i < this.pathLen; i++) {
        newPath.push(getRandomInt(4))
      }
      this.path = newPath

      //start round
      this.nextRound()

    },
    nextRound(){
      this.wait = false
      this.pathCursor = 0
      if(this.roundsLeft<1){
        this.putWinLoseMessage(false)
        return
      }
      setTimeout(()=>this.startPath(), 1000)
    },
    startPath(){
      let delay = this.getDelayFromDifficult(this.difficult)
      let nowPathLen = this.getNowPathLen()
      for (let i = 0; i < nowPathLen; i++) {
        let time = 1000*delay*i
        setTimeout(()=>{
          this.light[this.path[i]] = true
          this.light = this.light.slice()
          this.makeSound(this.srcSounds[this.path[i]])
        },time)
        setTimeout(()=>{
          this.light = [...allOffLight]
          if(i === nowPathLen-1) this.wait = true
        },time+this.lightTime)
      }

    },

    clickSimonBtn(num){
      if(num<0 || num>3 || !this.wait) return
      this.makeSound(this.srcSounds[num])
      if(this.path[this.pathCursor] === num){
        this.pathCursor++
        if(this.pathCursor === this.getNowPathLen()){
          this.roundsLeft--
          this.nextRound()
        }
      }
      else this.putWinLoseMessage(true)
    },


  }
}
</script>

<style scoped>

  .game{
    width:500px;
    aspect-ratio: 1/1;
    background-color: white;

    display: grid;
    place-items: center;
    position: relative;

    border-radius: 16px;
    box-shadow: 0 0 39px 30px rgba(15, 255, 0, 0.34);
  }


  .messageStyle{
    position: absolute;
    top:60px;
    left: 10px;
    width: 200px;
    height: 40px;

    display: grid;
    place-items: center;
    border: 2px solid lightgreen;
  }
  .messageStyle.loseMessage{
    border-color: orangered;
  }

  .controls{
    position: absolute;
    top: 0;
    left: 0;
    width: 35%;

    display: flex;
    justify-content: space-between;
    padding: 10px;
  }

</style>