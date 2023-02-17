<template>
    <div class="aProposDeMoi" v-on:mouseenter="createSpan()">
        <div>
            <p>
                <span :style="{animationDelay : timer + 0.01 * index + 's'}" class="wordAppearing" v-for=" (word, index )  in presentationSplitInArray" :key="index">{{ word}}</span>
            </p>
            <ul>
                <li><span :style="{animationDelay : 0.01 * index + 's'}" class="letterAppearing" v-for=" (word, index )  in presentationMailLetterArray" :key="index">{{ word}}</span></li>
            </ul>
        </div>
        <img class="background" src="@/assets/bg.png" alt="background">
    </div>
  </template>
  
  <script>
  export default {
    name: 'APropos',
    props:{
    },
    components:{
    },
    data(){
        return{
            skills:{'dev' : ["VueJS","NuxtJS", "Javascript", "SQL", "ThreeJS", "NodeJS"], 'proj' : ["git (Github)", "AGILE"], 'prog' : ["Python", "C++", "OpenGL"]}, //, "Javascript", "SQL", "ThreeJS", "NodeJS"], ["git (Github)", "AGILE"],["Python", "C++", "OpenGL"]],
            presentationSplitInArray : "",
            presentationMailLetterArray : "",
            timer : 0,
            presentationSpeech : "Salut! Je suis Solem Tchangaï, une ingénieure passionnée par le développement web. Les frameworks Javascript c'est mon dada. J'aime travailler en équipe et je suis toujours à l'écoute pour aider les autres. N'hésitez pas à me contacter si vous avez des questions ou si vous voulez discuter d'un projet ensemble!",
            presentationMail : "solem.tchangai@orange.fr"
        }
    },
    created: function() {
		
	},
    mounted(){
        this.createSpan();
    },
    methods:{
        createSpan: function(){
            console.log("hello de APropos")
            this.presentationSplitInArray = this.MakeSpan(this.presentationSpeech, " ");
            this.presentationMailLetterArray = this.MakeSpan(this.presentationMail, "");
        },
        MakeSpan: function(string, separateur){
            // let presentation = "Salut! Je suis Solem Tchangaï, une ingénieure passionnée par le développement web. Les frameworks Javascript c'est mon dada. J'aime travailler en équipe et je suis toujours à l'écoute pour aider les autres. N'hésitez pas à me contacter si vous avez des questions ou si vous voulez discuter d'un projet ensemble!"
            return string.split(separateur);
        },
    }
  }
  </script>
  
  <style scoped>
.background{
    position:absolute;
    bottom: -40vh;
    left:-10vw;
    height:120%;
    transform: rotate(35deg);
}

p, li{
    /* font-family: 'Questrial'; */
    font-size: 1.5rem;
    text-transform: uppercase;
    width: 65vw;
    margin-left: 5vw;
    display: flex;
    justify-content: flex-end; 
}

p{
    font-family: 'Questrial';
    font-size: 2rem;
    text-align: right;
}
h2{
    margin: 1vh 10vw;
    font-size: 5rem;
}

h3{
    margin:1vh 1vw;
    font-size: 2rem;
    background-color: black;
}

ul{
    margin:1vh 1vw;
    list-style: none;
    position: relative;
    z-index: 1;
}

.aProposDeMoi{
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    height: 100vh;
    justify-content: flex-start;
    width: 100vw;

}

.aProposDeMoi div{
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    justify-content: space-around;
    margin: 1vh 10vw;
    text-align: justify;
    min-height:100%;
    min-width:100%;
}

.aProposDeMoi p{
    max-height:450px;
    max-width:1000px;
    display:flex;
    flex-wrap: wrap;
    justify-content: right;

    position: relative;
    z-index: 10;
}
@keyframes AnimatedPresentation{
  0% { transform: translate3d(0, 50%, 0);
        opacity: 0; }
    50%{opacity: 0;}
  100% { transform: translate3d(0, 0%, 0);
            opacity:1; }
}
.wordAppearing{
    margin:0 5px;
    opacity:0;
    animation : AnimatedPresentation 1.5s ease forwards;
    /* animation-delay: 1s; */
    /* transform: translate3d(0,100%, 0); */
    animation-fill-mode: forwards;
    line-height: 1.2;
    font-size: 2.1rem;
}

@keyframes AnimatedLetter{
0%{transform: translate3d(50%, 0, 0); opacity:0;}
50%{opacity:0;}
100%{transform: translate3d(0,0,0); opacity: 1;}
}
.letterAppearing{
    font-family: 'Questrial';
    opacity:0;
    animation : AnimatedLetter 1.5s ease forwards;
    /* animation-delay: 1s; */
    /* transform: translate3d(0,100%, 0); */
    animation-fill-mode: forwards;
    font-size: 4.5rem;

}

  </style>