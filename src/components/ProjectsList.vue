<template>
    <div class="list">
        <div v-for="project in projectsData" :key="project.id">
            <ProjectCard :title="project.title" :image="project.image" :description="project.description" :video="project.video" :sousTitre="project.sousTitre" />
        </div>
    </div>
</template>
<script>
import ProjectCard from './ProjectCard.vue'
export default{
    name : 'ProjectsList',
    components:{
        ProjectCard
    },
    props:{
        
    },
    data(){
        return{
            projectsData : [
                {id:0, title:"Moodboard", image:require('@/assets/projects/moodboard/image-moodboard.png'), sousTitre:"VueJS - 2021", video:require('@/assets/projects/moodboard/moodboard_compressed.mp4'), description:"Moodboard est un site de création de moodboards via des mots-clé ou une couleur. Moodboard est codé en javascript sur le framework Vue.js. (2021)"},
                {id:1, title:"Recoding Project", image:require('@/assets/projects/p5/image-p5.png'), sousTitre:"P5 - 2020", video:require('@/assets/projects/p5/recoding_compressed.mp4')},
                {id:2, title:"Chasse-Taupes", image:require('@/assets/projects/taupes/image-taupes.png'), sousTitre:"VueJS - 2021", video:require('@/assets/projects/taupes/taupes_compressed.mp4'), description:"Ce  projet  est un jeu de chasse-taupes codé en javascript en utilisant le framework VueJS. Pour ce jeu, nous avons respecté plusieurs lois mathématiques relatives à l’aléatoire (lois exponentielle, géométrique, loi de Bernouilli et de Poisson). (2021)"},
                {id:3, title:"project4", image:require('@/assets/logo.png'), description:"description1blablabla blabla blabla bla"},
            ],
        }
    }
}
</script>
<style scoped>
.list{
    width:86%;
    height:fit-content;
    margin:0 7% 3vh 10%;

    display:flex;
    flex-wrap: wrap;
    justify-content: space-around;
    row-gap: 3vh;

    overflow-y: scroll;
    padding-right: 300px;
    box-sizing: content-box;
}

.list>div{
    width:fit-content;
}
</style>