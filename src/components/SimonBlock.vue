<template>
  <div class="simon">
    <div :class="{...style, red:true, active:light[0],isPlay:this.isWait}" @click="()=>{next(0)}"></div>
    <div :class="{...style, yellow:true, active:light[1],isPlay:this.isWait}" @click="()=>{next(1)}"></div>
    <div :class="{...style, green:true, active:light[2],isPlay:this.isWait}" @click="()=>{next(2)}"></div>
    <div :class="{...style, blue:true, active:light[3],isPlay:this.isWait}" @click="()=>{next(3)}"></div>
  </div>
</template>

<script>
export default {
  props:["light","isWait", "next"],
  data(){
    return {
      style:{gameBtn:true}
    }
  },
  methods:{
    clickBtn(){
      console.log("hello")
    }
  }
}
</script>

<style scoped>

.simon{
  background-color: white;
  width: 250px;
  aspect-ratio: 1/1;
  position: relative;
  border-radius: 50%;
}

.gameBtn{
  width: 50%;
  aspect-ratio: 1/1;
  position: absolute;
  opacity: 0.4;
  /*border: 3px solid black;*/
}



.gameBtn.active,.gameBtn.isPlay:active{
  opacity: 1;
}

.gameBtn.isPlay{
  cursor: pointer;
}


.gameBtn.red{
  /*border-color: red;*/
  background-color: #ff5050;

  /*left up*/
  top: 0;
  left: 0;
  border-top-left-radius: 100%;

}
.red:hover{
  border-top: 3px solid black;
  border-left: 3px solid black;
}

.gameBtn.yellow{
  /*border-color: yellow;*/
  background-color: yellow;

  /*right up*/
  top: 0;
  right: 0;
  border-top-right-radius: 100%;
}

.yellow:hover{
  border-top: 3px solid black;
  border-right: 3px solid black;
}

.gameBtn.blue{
  /*border-color: blue;*/
  background-color: #2bc9fa;

  /*left bottom*/
  bottom: 0;
  left: 0;
  border-bottom-left-radius: 100%;
}

.blue:hover{
  border-bottom: 3px solid black;
  border-left: 3px solid black;
}
.gameBtn.green{
  /*border-color: green;*/
  background-color: #4fff4f;

  /*right bottom*/
  bottom: 0;
  right: 0;
  border-bottom-right-radius: 100%;
}
.green:hover{
  border-bottom: 3px solid black;
  border-right: 3px solid black;
}
</style>