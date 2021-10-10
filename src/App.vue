<template>
<button @click="startGame" :disabled="isPlaying" class="btn">Play</button>
<Block v-if="isPlaying" :delay="delay" @end="endGame"></Block>
<Result :score="score" v-if="!isPlaying"></Result>
</template>
<script>
import Block from './components/Block.vue'
import Result from "./components/Result.vue"
export default {
  name: 'App',
  components: {
    Block,
    Result
  },
  data(){
    return{
      isPlaying:false,
      delay:null,
      score:0,
    }
  },
  methods: {
    startGame(){
      this.isPlaying=true
      this.delay=1000+Math.random()*3000
    },
    endGame(reactionTime){
      this.score=reactionTime
      this.isPlaying=false

    }
  },
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
:root{
  --success:green;
  --danger:crimson;
  --dark:black;
  --light:#FFFFFF;
  --radius:10px;
}
*{
  box-sizing: border-box;
}
.btn{
  height: 46px;
  padding: 0 20px;
  background: var(--success);
  color:var(--light);
  border:1px solid transparent;
  outline:none;
  border-radius: var(--radius);
    display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px auto;
  cursor: pointer;
}
.btn--danger{
  background: var(--danger);
}
.btn--delete{
  margin-top:100px;
}
[disabled]{
  cursor: not-allowed;
  opacity: .2;
}
li{
  list-style: none;
  text-align: left;
}
ul{
  padding: 0;
}

</style>
