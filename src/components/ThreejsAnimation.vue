<template>
  <div id="container">

  </div>
</template>

<script>
import * as Three from "three"
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'
export default {
  name: 'ThreeAnimation',
  props:{
    getCommands : Boolean,
    rotation:Number
  },
  data() {
    return{
      camera : null,
      scene : null,
      renderer : null,
      mesh : null,
      mouse : null,
      target : null,
      windowHalf : null,
      selectedObject:null,
      raycaster : null,
      pages : null,
      orbit : null,
      bgMesh : null,
    }
  },
  watch:{
    rotation:function(IsRotating){
      
        console.log("threejsAnimation rotation " + IsRotating)
        // this.orbit.target = new Three.Vector3(0,0,0); // set the center
        // this.orbit.maxPolarAngle =  Math.PI/2; // prevent the camera from going under the ground
        // this.orbit.minDistance = 80; // the minimum distance the camera must have from center
        // this.orbit.maxDistance = 150; // the maximum distance the camera must have from center
        // this.orbit.zoomSpeed = 0.3; // control the zoomIn and zoomOut speed
        // this.orbit.rotateSpeed = 0.3; // control the rotate speed
        this.orbit.autoRotate = IsRotating == 1 ? true : false;
        //this.$emit("update:rotation", IsRotating == 1 ? 0 : 1)
      
      

      // this.camera.rotation.y += Math.PI/3 * newRotation;

      // //this.camera.position.y += 50;
      // this.camera.position.z += temp;
      //this.$emit("update:rotation", 0)
    }
  },
  methods:{
    onMouseMove: function(event){
      this.mouse.x = ( event.clientX / window.innerWidth ) * 2 - 1;
      this.mouse.y = - ( event.clientY / window.innerHeight ) * 2 + 1;
      this.raycaster.setFromCamera(this.mouse, this.camera);
      var intersects = this.raycaster.intersectObjects(this.scene.children);
      
      if (intersects.length > 0) {
        this.selectedObject = intersects[0];
        console.log(this.selectedObject.object.name);
        if(this.pages.find(element => element == this.selectedObject.object.name)){ // maybe put the value selectedObject in a watch observator : when it changes of value then the cursor return to normal
          //console.log("#" + this.selectedObject.object.name)
          document.body.style.cursor = "pointer";
        }
        
      }else{
          document.body.style.cursor = "auto"
        }
    },
    onMouseWheel: function(event){

        if(this.camera.position.z >= 0){
          this.camera.position.z += event.deltaY * 0.5; // move camera along z-axis
        }else{
          this.camera.position.z = 0.2
        }

        if(this.camera.position.z >= 120){
          this.camera.position.z = 119
        }

        // if(this.camera.position.z > 140){

        //   this.$emit("update:getCommands", true)
        // }else{
        //   this.$emit("update:getCommands", false)
        // }

    },
    onResize: function(){
      const width = window.innerWidth;
      const height = window.innerHeight;
      
      this.windowHalf.set( width / 2, height / 2 );
      
      this.camera.aspect = width / height;
      this.camera.updateProjectionMatrix();
      this.renderer.setSize( width, height );
    },
    init: function() {
        let container = document.getElementById('container');

        this.camera = new Three.PerspectiveCamera( 45, window.innerWidth / window.innerHeight, 0.1, 500);
        this.camera.position.z = 150;

        this.scene = new Three.Scene();

        // LIGHT
        // var light = new Three.PointLight(0xffffff);
        // light.position.set(0,250,0);
        // this.scene.add(light);

 
        const geometry = new Three.SphereGeometry( 10, 32, 16 );
        const material = new Three.MeshNormalMaterial({ opacity: 0.95, transparent: true});

        
        for ( let i = 0; i < 15; i ++ ) {
        
          const object = new Three.Mesh( geometry, material );
          object.position.x = Math.random() * 100 - 50;
          object.position.y = Math.random() * 80 - 40;
          object.position.z = Math.random() * 100 - 50;
          object.rotation.x = Math.random() * 2 * Math.PI;
          object.rotation.y = Math.random() * 2 * Math.PI;
          object.rotation.z = Math.random() * 2 * Math.PI;
          if(i < this.pages.length){
            object.name = this.pages[i]
          }
          console.log(object.name);
          this.scene.add( object );
              
        }
        
        
        const loader = new Three.TextureLoader();
        const texture = loader.load(
          require('@/assets/Nebula.png'),
        );
        texture.magFilter = Three.LinearFilter;
        texture.minFilter = Three.LinearFilter;

        const shader = Three.ShaderLib.equirect;
        const materialBG = new Three.MeshNormalMaterial({color: 0x020202 })
        const materialSky = new Three.ShaderMaterial({
          fragmentShader: shader.fragmentShader,
          vertexShader: shader.vertexShader,
          uniforms: shader.uniforms,
          depthWrite: false,
          side: Three.BackSide,
        });
        materialSky.uniforms.tEquirect.value = texture;
        const plane = new Three.BoxGeometry(2, 2, 2);
        this.bgMesh = new Three.Mesh(plane, materialBG);
        this.bgMesh.visible = false;
        this.scene.add(this.bgMesh);
        

        this.renderer = new Three.WebGLRenderer( { antialias: true } );
        this.renderer.setSize( window.innerWidth, window.innerHeight );

        /**** ORBIT CAMERA */
        this.orbit = new OrbitControls(this.camera, this.renderer.domElement);
        this.orbit.target = new Three.Vector3(0,0,0); // set the center
        this.orbit.maxPolarAngle =  Math.PI/2; // prevent the camera from going under the ground
        this.orbit.minDistance = 80; // the minimum distance the camera must have from center
        this.orbit.maxDistance = 120; // the maximum distance the camera must have from center
        this.orbit.zoomSpeed = 0.3; // control the zoomIn and zoomOut speed
        this.orbit.rotateSpeed = 0.3; // control the rotate speed
        this.orbit.autoRotate = true;

        container.appendChild( this.renderer.domElement );
        
        container.addEventListener( 'mousemove', this.onMouseMove, false );
        container.addEventListener( 'wheel', this.onMouseWheel, false );
        window.addEventListener( 'resize', this.onResize, false );

    },
    animate: function() {
        /*** move the camera with the mouse ***/
        // this.target.x = ( 1 - this.mouse.x ) * 0.2;
        // this.target.y = ( 1 - this.mouse.y ) * 0.2;
      
        // this.camera.rotation.x += 0.5 * ( this.target.y - this.camera.rotation.x );
        // this.camera.rotation.y += 0.5 * ( this.target.x - this.camera.rotation.y );
        //console.log(this.camera.rotation.x)
        requestAnimationFrame( this.animate );
        this.orbit.update();

        this.bgMesh.position.copy(this.camera.position);
        
        this.renderer.render( this.scene, this.camera );
    }
  },
  mounted() {
    this.mouse = new Three.Vector2();
    this.target = new Three.Vector2();
    this.windowHalf = new Three.Vector2( window.innerWidth / 2, window.innerHeight / 2 );
    this.raycaster = new Three.Raycaster();
    this.pages = ["projects", "introduction", "contact", "hightlight1"]
    
    this.init();
    this.animate();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#container{
  width: 100%;
  height:100%;
}
</style>
