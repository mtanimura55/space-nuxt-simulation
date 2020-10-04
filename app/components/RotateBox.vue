<template>
  <div ref="rotatebox" />
</template>

<script>
import * as THREE from 'three'

export default {
  name: 'RotateBox',
  data() {
    const scene = new THREE.Scene()
    const renderer = new THREE.WebGLRenderer()
    const camera = new THREE.PerspectiveCamera(75, 600 / 400, 0.1, 1000)
    const light = new THREE.DirectionalLight(0xffffff)
    const geometry = new THREE.BoxGeometry(1, 1, 1)
    const material = new THREE.MeshNormalMaterial()
    const cube = new THREE.Mesh(geometry, material)
    const width = window.innerWidth
    const height = window.innerHeight
    return {
      scene,
      renderer,
      camera,
      light,
      geometry,
      material,
      cube,
      width,
      height,
    }
  },
  mounted() {
    this.camera.position.set(0, 0, 2)
    this.light.position.set(0, 0, 10)
    this.scene.add(this.cube)
    this.scene.add(this.light)

    this.resize()
    this.animate()

    this.$refs.rotatebox.appendChild(this.renderer.domElement)

    // windowのサイズ変更イベントを検知
    window.addEventListener('resize', this.resize)
  },
  methods: {
    animate() {
      requestAnimationFrame(this.animate)

      this.cube.rotation.x += 0.02
      this.cube.rotation.y += 0.02

      this.renderer.render(this.scene, this.camera)
    },
    resize() {
      // 変更時のwindowサイズを取得
      this.width = window.innerWidth
      this.height = window.innerHeight

      // レンダラーのサイズを調整する
      this.renderer.setPixelRatio(window.devicePixelRatio)
      this.renderer.setSize(this.width, this.height)

      // カメラのアスペクト比を正す
      this.camera.aspect = this.width / this.height
      this.camera.updateProjectionMatrix()
    },
  },
}
</script>

<style></style>
