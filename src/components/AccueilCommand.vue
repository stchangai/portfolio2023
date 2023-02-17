<template>
    <div class="command">
        <img class="arrowCommand" id="arrowCommandL"  src="@/assets/icons/down_arrow.svg" alt="left arrow to rotate around the three.js spheres" v-on:click="Rotate()"/>
        <img class="arrowCommand" id="arrowCommandR" src="@/assets/icons/down_arrow.svg" alt="right arrow to rotate around the three.js spheres" v-on:click="Rotate()"/>
    </div>
</template>
<script>
export default{
    name : 'AccueilCommand',
    props:{
        side : String,
        rotation : Number,
    },
    data(){
        return{
            IsRotating : 0
        }
    },
    methods:{
        Rotate: function(){
            this.IsRotating == 0 ? this.IsRotating = 1 : this.IsRotating = 0
            console.log("rotate " + this.IsRotating)
            // if(this.IsRotating == 0){console.log("hello");this.IsRotating = 1}
            // else{
            //     console.log('bye');this.IsRotating = 0;
            // }
            this.$emit("update:rotation", this.IsRotating)
        }
    }
}
</script>
<style scoped>
.command{
    position:absolute;
}
.arrowCommand:hover{
    cursor:pointer;
}
#arrowCommandL{
    transform: rotate(90deg);
    position :absolute;
    top: 50vh;
    left: 10vw;
    height: 40px;
    width: 40px;
    filter: invert(100%) sepia(1%) saturate(622%) hue-rotate(210deg) brightness(119%) contrast(100%);
}

#arrowCommandR{
    transform: rotate(-90deg);
    position :absolute;
    top: 50vh;
    left: 90vw;
    height: 40px;
    width: 40px;
    filter: invert(100%) sepia(1%) saturate(622%) hue-rotate(210deg) brightness(119%) contrast(100%);
}
</style>