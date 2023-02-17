<template>
  <div id="app">
    <MainSection title="Portfolio" nextpage="projects"/>
    <MainSection title="Projects" />
    <MainSection title="A Propos" v-on:mouseenter="createSpan()" :enterpage="InAProposPage"/>
    <MainSection title="Competences"/>
  </div>
</template>

<script>
import MainSection from './components/MainSection.vue'

export default {
  name: 'App',
  components: {
    MainSection
  },
  data(){
    return{
      IsPortfolioOpen : false,
      InAProposPage : false
    }
  },
  methods:{
    createSpan : function(){
      console.log('hello')
      this.InAProposPage = true
    }
  }
}
</script>

<style>

@font-face {
    font-family: "BigJohn";  
    src: local("BigJohn"), url(./assets/fonts/BigJohn-Bold.otf) format("opentype");
}

html, body {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  scroll-behavior: smooth;
  scroll-snap-type: y mandatory;
}
html{
  overflow-y: hidden;
}
body{
  display:flex;
}
#app {
  box-sizing: border-box;
  font-family: "BigJohn", Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  display: flex;
  flex-direction: column;
  margin: 0;
  padding: 0;
  border: 0;
  width: 100%;

  scroll-snap-type: y mandatory;	
	-webkit-overflow-scrolling: touch;
}

@media screen and (max-width: 900px){
  #app .section{
    font-size:300%;
  }
  .list{
    column-gap: 5vw;
  }
  #app .threejs {
    margin-left: 0%;
  }
  .skillName{
    margin-top: 3vh;
    margin-bottom: 1vh;
  }
  .skillIntro{
    margin-top: 3vh;
  }
  #app .wordAppearing{
    animation: none;
    opacity:1;
  }
  #app .letterAppearing{
    animation:none;
    opacity:1;
  }
  #competences h1{
    font-size: 1.6em;
    margin-top: 5vh;
  }
}

@media screen and (max-width: 600px){
  #app .section{
    font-size:250%;
  }
  .list{
    column-gap: 10vw;
  }
  #app .under{
    width:70vw;
  }
  #app .presentation{
    font-size: 1.1rem;
  }
  #app .animationText > div{
    height:55%;
  }
  #app .projectCard{
    width:60vw;
  }
  #app .background{
    height:90%;
  }
  #competences .background{
    top:-50vh;
  }
  #app .aProposDeMoi p{
    position: relative;
    z-index: 10;
    
  }
  #app .aProposDeMoi span{
    font-size: 1.5rem;
  }
  #app .aProposDeMoi div{
    justify-content: flex-start;
  }
  #app .wordAppearing{
    animation: none;
    opacity:1;
  }
  #app .letterAppearing{
    animation:none;
    opacity:1;
  }
}

@media screen and (max-width: 400px){
  #app .section{
    font-size:170%;
  }
  #app .presentation{
    font-size: 1rem;
  }
  #app .animationText > div{
    height: 62%;
  }
  #app .animationText > div.text-top-top{
    height: 35%;
  }
  #app .under{
    width:80vw;
  }
  #app .projectCard{
    width:60vw;
  }
  #app .background{
    height:90%;
  }
  #competences .background{
    top:-50vh;
  }
  #app .aProposDeMoi p{
    position: relative;
    z-index: 10;
    
  }
  #app .aProposDeMoi span{
    font-size: 1.2rem;
  }
  #app .aProposDeMoi div{
    justify-content: space-evenly;
  }
  #app .skillIntro{
    font-size: 1.2rem;
  }
  #app .wordAppearing{
    animation: none;
    opacity:1;
  }
  #app .letterAppearing{
    animation:none;
    opacity:1;
  }
}
</style>
