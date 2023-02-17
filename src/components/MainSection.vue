<template>
    <div class="section snap" :id="title.toLowerCase()">
        
        <!-- <h2 class="presentation upper desktop">Bienvenue sur mon</h2> -->
        <h1 v-if="title.toLowerCase() != 'portfolio'">{{ title.toUpperCase() }}</h1>
        <AnimationText v-if="title.toLowerCase() == 'portfolio'" class="text" :title="title" />
        <!-- <h3 class="presentation under desktop">Je m'appelle Solem Tchangaï, actuellement en dernière année d'école d'ingénieur. <br>Je suis heureuse de vous accueillir dans mon univers.</h3> -->
        <ThreejsAnimation class="threejs" v-if="title.toLowerCase() == 'portfolio'" v-bind:getCommands.sync="getCommands" v-bind:rotation.sync="rotation"/>
        <AccueilCommand v-show="getCommands" v-bind:rotation.sync="rotation"/>
        <ProjectsList v-if="title.toLowerCase() == 'projects'" />
        <APropos v-if="title.toLowerCase() == 'a propos'" />
        
        <CompetencesList v-if="title.toLowerCase() == 'competences'" />
        <a v-if="nextpage != undefined" :href="'#'+nextpage" v-on:click="OpenPortfolio" class="animatedArrows"><img class="downArrowIcon" src="@/assets/icons/down_arrow.svg" alt="down arrow to swipe to the next section"><img class="downArrowIcon" src="@/assets/icons/down_arrow.svg" alt="down arrow to swipe to the next section"></a>
    </div>
</template>
<script>
import ProjectsList from "./ProjectsList.vue"
import ThreejsAnimation from "./ThreejsAnimation.vue"
import AccueilCommand from "./AccueilCommand.vue"
import AnimationText from "./AnimationText.vue"
import APropos from "./APropos.vue"
import CompetencesList from "./CompetencesList.vue"
export default{
    name : 'MainSection',
    components:{
        ProjectsList,
        ThreejsAnimation,
        AccueilCommand,
        AnimationText,
        APropos, 
        CompetencesList,
    },
    props:{
        title :String,
        nextpage: String,
        enterpage : Boolean,
    },
    data(){
        return{
            getCommands : false,
            rotation: 1
        }
    },
    methods:{
        OpenPortfolio:function(){
            document.documentElement.style.overflowY = "auto";
        },
    },
}
</script>
<style scoped>




.section{
    height: 100vh;
    /* min-height: 100vh; */
    /* height:fit-content; */
    max-width:100%;
    width: 100vw;
    background-color : black;
    font-size: 5rem;
    font-family: 'BigJohn','Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color:rgb(230, 224, 224);
    
    margin: 0;
    padding: 0;
    border: 0;

    display: flex;
    flex-direction: column;
    align-items: flex-start;

    position:relative;
    overflow: hidden;
    scroll-snap-type: y mandatory;
}

.snap{
    scroll-snap-align: start;
}

#competences{
    display:flex;
    /* justify-content: space-between; */
    /* align-items: center; */
}   

#apropos{
    position:relative;
}

.threejs{
    margin-left:20%;
}

.threejsAbsolute{
    position: absolute;
    top: 0;
    margin-right: 50vh;
}

h1{
    color:white;
    margin-left: 5vw;
    margin-bottom: 2vh;
    font-family: 'BigJohn','Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    position:relative;
    z-index: 1;
}

a{
    height: fit-content;
    width: fit-content;
}

.downArrowIcon{
    position :absolute;
    bottom: 5vh;
    left:50%;
    height: 40px;
    width: 40px;
    filter: invert(100%) sepia(1%) saturate(622%) hue-rotate(210deg) brightness(119%) contrast(100%);
}

.downArrowIcon + img {
    bottom: 4vh;
}

@keyframes MoveArrowUp {
  0% { transform: translate3d(0, 100%, 0) scale(1); }
  50% { transform: translate3d(0, 20%, 0) scale(1.2); }
  100% { transform: translate3d(0, 100%, 0) scale(1); }
}

@keyframes MoveArrowDown {
  0% { transform: translate3d(0, 100%, 0) scale(1); }
  50% { transform: translate3d(0, 50%, 0) scale(1.1); }
  100% { transform: translate3d(0, 100%, 0) scale(1); }
}

.animatedArrows img{
    animation-iteration-count: infinite;
    animation-timing-function: ease;
}
.animatedArrows img:first-child{
    animation: MoveArrowUp 3s;
    /* animation-delay: 0.5s; */
    transform: translate(0, 100%);
    animation-iteration-count: infinite;
}
.animatedArrows img:last-child{
    animation: MoveArrowDown 3s;
    /* animation-delay: 1s; */
    transform: translate(0, 100%);
    animation-iteration-count: infinite;
}
</style>