<template>
    <div class="animationText">
        <div class="text-top-top">
            <div>
                <h2 class="presentation upper desktop top">Bienvenue sur mon</h2>
            </div>
        </div>
        <div class="text-top">
            <div>
                <h1 class="top">{{ title.toUpperCase() }}</h1>
            </div>
        </div>
        <div class="text-bottom">
            <h3 class="presentation under desktop">Je m'appelle Solem Tchangaï, actuellement en dernière année d'école d'ingénieur. <br>Je suis heureuse de vous accueillir dans mon univers.</h3>
        </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'AnimationText',
    props:{
        title : String
    }
  }
  </script>
  
  <style scoped>
@keyframes showTopText {
  0% { transform: translate3d(0, 100%, 0); }
  100% { transform: translate3d(0, 50%, 0); }
}
@keyframes showBottomText {
  0% { transform: translate3d(0, -200%, 0); }
  100% { transform: translate3d(0, 0, 0); }
}
.animationText {
  color:white;
  height:100vh;
  position: absolute;
  width: 100vw;
}
.animationText > div {
  height: 50%;
  overflow: hidden;
  position: absolute;
  width: 100%;
}
.animationText > div div {
  /* font-size: 12vmin; */
  padding: 2vmin 0;
  position: absolute;
}
.animationText > div div .top {
  display: block;
}
.animationText > div.text-top {
  /* border-bottom: 1vmin solid #000; */
  top: 0;
}
.animationText > div.text-top div {
  animation: showTopText 1s;
  animation-delay: 1s;
  animation-fill-mode: forwards;
  bottom: 0;
  transform: translate(0, 100%);
  height:100%;
}


.animationText > div.text-top-top {
  /* border-bottom: 1vmin solid #000; */
  height:25%;
  top: 0;
}
.animationText > div.text-top-top div {
  animation: showTopText 1s;
  animation-delay: 0.5s;
  animation-fill-mode: forwards;
  bottom: 0;
  transform: translate(0, 100%);
  height:100%;
}

/* .animationText > div.text-top div h2 {
  color: #767676;
} */
.animationText > div.text-bottom {
  bottom: 0;
}
.animationText > div.text-bottom h3 {
  animation: showBottomText 1s;
  animation-delay: 2s;
  animation-fill-mode: forwards;
  top: 0;
  transform: translate(0, -200%);
}

.presentation{
    font-family: 'Questrial';
    /* position:absolute; */
    /* top: 0; */
    margin: 5vh;
    font-size: 1.2rem;
}

.upper{
    /* top: 25vh; */
    font-size: 1.5rem;
}

.under{
    /* top : 55vh; */
    width:45vw;
    text-align: start;
    line-height: 1.5;
}

h1{
    color:white;
    /* position:absolute;
    top:35vh; */
    margin : 0 0 5vh 5vh;
    letter-spacing: 1px;
    /* z-index: 100; */
    font-family: 'BigJohn','Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}


  </style>
  