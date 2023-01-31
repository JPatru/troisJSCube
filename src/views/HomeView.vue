<template>
  <Renderer ref="renderer" antialias resize="window" :orbit-ctrl="{ autoRotate: true, enableDamping: true, dampingFactor: 0.05 }">
    <Camera :position="{ z: 10 }" />
    <Scene ref="scene" :background="sceneColor">
      <Raycaster ref="raycaster" intersect-mode="frame" @pointerOver="onPointerOver" @click="onClick"
      />
      <PointLight :intensity="1" :position="{ x: 0, y: 8, z: 5 }" />
      <PointLight :intensity="1" :position="{ x: -10, y: -3, z: 2 }" />
      <PointLight :intensity="1" :position="{ x: 6, y: -15, z: -6 }" />
      <Box :position="{ y: 0, z: 0 }">
        <PhongMaterial  :color="boxColor" />
      </Box>
      <template v-for="i in n" :key="i" >
        <template v-for="j in n" :key="j" >
          <Box ref="box" v-for="k in n" :key="k" :position="{ x: i-2, y: j-2, z: k-2 }">
            <PhongMaterial :color="boxColorLayer" />
          </Box>
        </template>
      </template>
    </Scene>
  </Renderer>
</template>

<script>
import { Scene, Renderer, Raycaster } from 'troisjs'
export default {
  components: {
    Raycaster
  },
  methods: {
    onClick({event}) {
      const raycaster = this.$refs.raycaster
      const box = this.$refs.box
      console.log("on est là", raycaster);
      // raycaster.pointer.intersectObjects(scene.children, false)
  }
  }
  

}
</script>



<script setup>
//
// IMPORTS
//
  import { ref } from 'vue'

//
// REFS
//
  const n = ref(3)
  const boxColor = ref("#dc143c")
  const boxColorLayer = ref("#285ebc")
  const sceneColor = ref("#f3f3f3")

//
// MOUSE OVER
//
  const onPointerOver = (event) => {
    let posx = event.component.mesh.position.x
    let posy = event.component.mesh.position.y
    let posz = event.component.mesh.position.z
    if (posx === 0 && posy === 0 && posz ===0  ) {
      event.component.mesh.material.color.set(event.over ? "#f24265" : "#dc143c")
    } else {
      event.component.mesh.material.color.set(event.over ? "coral" : "#285ebc")
    }
    
  }


//
// MOUSE CLICK
//
  const boxClick = (e) => {
      // alert('Click');
      console.log(e);
    }

</script>