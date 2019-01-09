<template>
  <div id="app">
    <div class="header">
      <h1>Paper Scissors Stone</h1>
    </div>
    <div class="score">
      <div class="user">user</div>
      <div class="comp">comp</div>
      <span class="score-user">{{user_score}}</span>:<span class="score-comp">{{comp_score}}</span>
    </div>
    <div class="result">
      <p>{{result}}</p>
    </div>
    <div class="choice">
      <div class="rock" >
        <img :src="stone" @click="choice('r')">
      </div>
      <div class="scissor">
        <img class="img-scissor" :src="scissor" @click="choice('s')">
      </div>
      <div class="paper">
        <img :src="paper" @click="choice('p')">
      </div>
    </div>
  </div>
</template>

<script>
import stone from '@/assets/stone.png'
export default {
  name: 'app',
  data() {
    return {
      stone:require('./assets/stone.png'),
      paper:require('./assets/paper.png'),
      scissor:require('./assets/scissor.png'),
      user_score:0,
      comp_score:0,
      result:"Choice your choice!!"
    }
  },
  methods: {
    choice(e){
      let user = e ;
      let comp = this.compchoice();
      let vm = this;
      switch(user + comp){
        case "rs":
        case "pr":
        case "sp":
          this.user_score++;
          let b=this.changeresult(user)
          let c=this.changeresult(comp)
          console.log("user win");
          this.result=b + " covers " + c+" .You Win!!"
          break;
        case "rp":
        case "ps":
        case "sr":
          this.comp_score++;
          b=this.changeresult(user)
          c=this.changeresult(comp)
          this.result=c + " covers " + b+" .You Lose!!"
          console.log("comp win");
          break;
        case "rr":
        case "pp":
        case "ss":
          b=this.changeresult(user)
          c=this.changeresult(comp)
          this.result=b + " draw " + c+" .Draw!!"
          console.log("draw");
          break;
      }
    },
    compchoice(){
      var comp=["r","s","p"];
      let comprandom=Math.floor(Math.random()*3);
      console.log(comp[comprandom])
      return comp[comprandom];
    },
    changeresult(letter){
      if(letter==="r") return "Rock"
      if(letter==="p") return "Paper"
        return "Scssiors"
    }
  },
  computed: {
    
  },
  mounted() {
    this.compchoice();
  },
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  position: fixed;
  background:gray;
  width: 100%;
  height: 100%;
}
.header{
  color:#25272E;
  padding:20px;
  background:white;
  font-family:sans-serif;
}
.choice{
  display:flex;
  flex-direction:row;
  justify-content:space-around;
}
.score{
  border:5px #FFAC55 solid;
  width:200px;
  height:60px;
  margin:20px auto;
  font-size:30px;
  position:relative;
  padding-top:8px;
}
.user{
  background-color:pink;
  font-size:15px;
  font-family:sans-serif;
  width:30%;
  position:absolute;
  top:15px;
  left:-30px;
}
.comp{
  background-color:pink;
  font-size:15px;
  font-family:sans-serif;
  width:30%;
  position:absolute;
  top:15px;
  right:-30px;
}
img{
  border-radius: 50%;
}
img:hover{
  transform: scale(1.1);
}
.result{
  margin:20px;
}
.result > p{
  font-size:40px;
}
</style>
