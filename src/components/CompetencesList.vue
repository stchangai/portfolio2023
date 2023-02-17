<template>
    <div class="skills"> 
        <div class="skill">
            <span class="skillIntro">En développement web, j'aime travailler avec et aimerais devenir une experte de ...</span>
            <!-- <h2 :style="{animationDelay: 2  * index + 's', animationDuration: 1.5 * (skills['dev'].length - index) + 's'}" class="rotatingText-adjective" v-for="(skilldev, index) in skills['dev']" :key="index">{{ skilldev }}</h2> -->
            <h2 class="skillName">{{ skills['dev'][counter] }}</h2>
        </div>
        <div class="skill">
            <span class="skillIntro">Je sais aussi utiliser ces languages...</span>
            <ul class="skillList">
                <li v-for="(skill, index) in skills['prog']" :key="index">{{ skill }}</li>
            </ul>
        </div>
        <div class="skill">
            <span class="skillIntro">Et je développe mes projets en utilisant :</span>
            <ul class="skillList">
                <li v-for="(skill, index) in skills['proj']" :key="index">{{ skill }}</li>
            </ul>
        </div>
        <img class="background" src="@/assets/bg.png" alt="background">
    </div>
  </template>
  
  <script>
  export default {
    name: 'CompetencesList',
    data(){
        return{
            skills:{'dev' : ["VueJS","NuxtJS", "Javascript", "SQL", "ThreeJS", "NodeJS"], 'proj' : ["git (Github)", "AGILE"], 'prog' : ["Python", "C++", "OpenGL"]}, //, "Javascript", "SQL", "ThreeJS", "NodeJS"], ["git (Github)", "AGILE"],["Python", "C++", "OpenGL"]],
            indexSkill : null,
            showSkills : false,
            randomPositions:[[[0,0,0,0], [0,0,0,0], [0,0,0,0],[0,0,0,0], [0,0,0], [0,0,0]], [[0,0,0],[0,0,0]], [[0,0,0], [0,0,0], [0,0,0]]],
            skillsVisible : [true, true, true],
            counter :  0,
            counterProg : 0, 
            counterProj : 0,
            
        }
    },
    created: function(){
        this.counter = this.skills['dev'].length;
        this.counterProg = this.skills['prog'].length;
        this.counterProj = this.skills['proj'].length
    },
    mounted(){
        this.TimerSkills();
    },
    methods:{
        timerDev : function(){
            if (this.counter >= 0) {
                    setTimeout(() => {
                        this.counter -= 1
                        // console.log(this.counter)
                        this.timerDev();
                        
                    }, 1000)
                    
                }else{
                    this.counter = this.skills["dev"].length;
                    this.timerDev()
                }
        },
        TimerSkills: function(){
                this.timerDev();
        },
    }
  }
  </script>
  
  <style scoped>
  .background{
    position: absolute;
    top: -80vh;
    left: -10vw;
    height: 120%;
    transform: rotate(35deg);
}
.skills{
    display:flex;
    flex-wrap: wrap;
    justify-content: center;
}
.skill{
    position:relative;
    display:flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 0 2vw;

    position: relative;
    z-index: 10;
}

.skill:first-child{
    flex-basis: 100%;
}

.skillIntro{
    font-family: 'Questrial';
    font-size: 1.5rem;
    text-transform: uppercase;
    text-align: center;
    margin-top: 5vh;
}

.skillName{
    min-height: 100px;
    font-size: 4rem;
}

.skillList{
    font-size: 1.2rem;
    list-style: none;
    display: flex;
}

.skillList li{
    margin: 0 2vw;
}

.rotatingText-adjective { 
  left: 0;
  margin-bottom: 0;
  margin-top: 30px;
  opacity: 0;
  position: absolute;
  right: 0;
  text-align: center;
  text-transform: uppercase;
  top: 40vh;
  animation : rotate-text-up 1.5s linear forwards;
  /* animation-iteration-count: infinite; */
}

@keyframes rotate-text-up { 
  0% {
    transform: translate3d(0, 80px, 0);
    opacity: 0;
  }
  
  20%, 80% {
    transform: translate3d(0, 0, 0);
    opacity: 1;
  }
  
  80% {
    transform: translate3d(0, -40px, 0);
    opacity: 0;
  }
  100%{
    transform: translate3d(0, 80px, 0);
    opacity: 0;
  }
}

  </style>