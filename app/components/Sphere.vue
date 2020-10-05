<template>
  <div ref="sphere" />
</template>

<script>
import * as THREE from 'three'

export default {
  name: 'Sphere',
  data() {
    const scene = new THREE.Scene()
    const renderer = new THREE.WebGLRenderer()
    const camera = new THREE.PerspectiveCamera(75, 600 / 400, 0.1, 1000)
    const light = new THREE.DirectionalLight(0xff0000)
    const geometry = new THREE.SphereGeometry(5)
    const material = new THREE.MeshBasicMaterial({
      map: new THREE.TextureLoader().load('/texture/sunSurfaceMaterial.jpg '),
    })
    const sphere = new THREE.Mesh(geometry, material)
    const width = window.innerWidth
    const height = window.innerHeight
    const step = 0
    const degree = 0
    const rad = 0
    return {
      scene,
      renderer,
      camera,
      light,
      geometry,
      material,
      sphere,
      width,
      height,
      step,
      degree,
      rad
    }
  },
  mounted() {
    this.camera.position.set(0, 200, 0)
    this.camera.lookAt(new THREE.Vector3(0, 0, 0))
    this.light.position.set(0, 0, 10)
    this.sphere.position.set(0, 0, 100)
    const axes = new THREE.AxesHelper(200)
    this.scene.add(this.sphere)
    this.scene.add(this.light)
    this.scene.add(axes)

    this.resize()
    this.animate()

    this.$refs.sphere.appendChild(this.renderer.domElement)

    // windowのサイズ変更イベントを検知
    window.addEventListener('resize', this.resize)
  },
  methods: {
    animate() {
      requestAnimationFrame(this.animate)

      this.sphere.rotation.x += 0.02
      this.sphere.rotation.y += 0.02

      // 角速度 ω = v/r
      // v = 1000 と過程。等速の場合
      // const v = 15
      // // r = 100 で設定。
      const r = 100
      // const r = this.sphere.getWorldPosition().z
      console.log("r:" + r)
      // this.degree += 1
      // const rad = this.degree * Math.PI / 180
      this.rad += 2 * Math.PI / 180;
      const rad = this.rad
      // console.log("degree:" + this.degree)
      console.log("rad:" + rad)
      console.log("Math.cos(rad):" + Math.cos(rad))
      console.log("Math.sin(rad):" + Math.sin(rad))

      this.sphere.position.x = r * Math.cos(rad)
      this.sphere.position.z = r * Math.sin(rad)
      console.log("x:" + this.sphere.position.x)
      console.log("z:" + this.sphere.position.z)
      this.step += 1

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
