<template>
    <div class="projectCard" :style="{background: 'no-repeat center url('+ image +')'}">
        <h1>{{ title }}</h1>
        <p class="projectSousTitre">{{ sousTitre }}</p>
        <label class="playVideo">
            <input v-model="PlayIsClicked" type="checkbox">
            <span class="iconPlay"><img src="@/assets/icons/play.svg" alt="icon video play"></span>
        </label>
        
        <div class="projectVideo" v-if="PlayIsClicked && video != 'undefined'" v-on:click="VideoOut">
            <h2 class="projectTitle">{{ title }}</h2>
            <video :class="{active : PlayIsClicked}" :poster="image" autoplay="true" preload="none" :src="video" controls="controls"></video>
            <span class="projectDescription">{{ description }}</span>
        </div>
        
    </div>
</template>
<script>
export default{
    name : 'ProjectCard',
    props:{
        title :String,
        image : String,
        description : String,
        video : String,
        sousTitre : String,
    },
    data(){
        return{
            PlayIsClicked:false,
        }
    },
    watch:{
        PlayIsClicked:function(NewPlayIsClicked){
            if(NewPlayIsClicked){
                console.log(NewPlayIsClicked + ' ==> ' + this.video)

            }
        }
    },
    methods :{
        VideoOut:function(){
            this.PlayIsClicked = false
        }
    }
}
</script>
<style scoped>
.projectCard{
    height:25vh;
    width: 25vw;
    display:flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: flex-start;

    padding:1vh 1vw;
}

h1{
    font-size: 1.5rem;
    margin-bottom: 0;
}

.projectSousTitre{
    font-size: 0.5rem;
    font-weight: 0;
}

span img{
    height:16px;
    width:16px;
    filter: invert(100%) sepia(1%) saturate(622%) hue-rotate(210deg) brightness(119%) contrast(100%);
    transition: transform 1s;
}

.playVideo{
    position: relative;
    display: inline-block;
    height: 16px;
    width: 16px;
}

.playVideo input{
    position:absolute;
    right:0;
    opacity: 0;
    width: 0;
    height: 0;

}

.playVideo span, .playVideo span>img{
    position:absolute;
    right:0;
    height: 16px;
    width: 16px;
}

input:hover + span>img {
    transform:scale(1.8);
}

/* input:checked + span>img {
    transform:scale(2.3);
} */

.projectVideo{
    position:fixed;
    z-index: 10;
    right:0;
    top:0;
    height:100vh;
    width:100vw;
    transition : height 2s, width 2s;
    background : rgba(0, 0, 0, 0.91);

    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;

}

.projectTitle{
    font-size: 3rem;
}

.projectDescription{
    font-size: 1rem;
    font-family: 'Questrial';
}
video{
    height:0;
    width:0;
    transition:height 2s, width 2s;
    margin-bottom: 5vh;
}

.active{
    height : 50%;
    width:50%;
}
</style>