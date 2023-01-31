<template>
  <Renderer ref="renderer" antialias resize="window" :orbit-ctrl="{ autoRotate: true, enableDamping: true, dampingFactor: 0.05 }">
    <Camera :position="{ z: 10 }" />
    <Scene>
      <PointLight :intensity="1" :position="{ x: 0, y: 3, z: 5 }" />
      <PointLight :intensity="1" :position="{ x: -10, y: -3, z: 2 }" />
      <PointLight :intensity="1" :position="{ x: 6, y: -3, z: -6 }" />
      <Box ref="box" @pointerOver="boxOver" @click="boxClick" :rotation="{ y: Math.PI / 4, z: Math.PI / 4 }">
        <LambertMaterial :color="boxColor" />
      </Box>
      <Box ref="box2" :position="{ x: 1, y: 2, z: 1 }" @pointerOver="boxOver" @click="boxClick" :rotation="{ y: Math.PI / 4, z: Math.PI / 4 }">
        <LambertMaterial :color="boxColor" />
      </Box>
    </Scene>
  </Renderer>
</template>

<script>
import { Box, Camera, LambertMaterial, PointLight, Renderer, Scene } from 'troisjs';
export default {
  components: { Box, Camera, LambertMaterial, PointLight, Renderer, Scene },
  data() {
    return {
      boxColor: '#ffffff',
    };
  },
  methods: {
    boxOver({ over }) {
      this.boxColor = over ? '#ff0000' : '#ffffff';
    },
    boxClick(e) {
      alert('Click');
      console.log(e);
    },
  },
};
</script>