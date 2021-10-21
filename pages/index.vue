<template>
  <div ref="container" class="c-app"></div>
</template>

<script>
import * as THREE from 'three'
// let renderer, scene, camera

export default {
  components: {},
  data() {
    return {}
  },
  mounted() {
    this.init()
  },
  methods: {
    init() {
      const scene = new THREE.Scene()
      const camera = new THREE.PerspectiveCamera(
        45,
        window.innerWidth / window.innerHeight,
        0.1,
        1000
      )

      camera.position.set(0, 0, 20)

      const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true })
      // renderer.setClearColor('bisque', 0.5)
      renderer.setSize(window.innerWidth, window.innerHeight)
      this.$refs.container.appendChild(renderer.domElement)

      const geometry = new THREE.SphereGeometry(5, 20, 50)
      // const material = new THREE.MeshBasicMaterial({ color: '#232225' })
      const material = new THREE.MeshPhongMaterial({
        color: '#33334c',
        opacity: 1,
      })
      material.transparent = true

      const sphere = new THREE.Mesh(geometry, material)

      const ambientLight = new THREE.AmbientLight(0x888888)
      // Create a new directional light
      const directionalLight = new THREE.DirectionalLight(0xfdfcf0, 1)
      directionalLight.position.set(20, 10, 20)
      scene.add(directionalLight)
      scene.add(ambientLight)
      scene.add(sphere)

      const animate = () => {
        requestAnimationFrame(animate)
        renderer.render(scene, camera)
      }
      animate()
    },
  },
}
</script>

<style lang="scss" scoped>
.c-app {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  min-height: 100vh;
  background: #33334c;
}
</style>
