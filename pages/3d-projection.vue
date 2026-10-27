<template>
  <div>
    <h2 class="article-header">3D PROJECTION</h2>
    <main class="main-content">
      <p>So we’ve tossed a 3D object through a 2D universe, but can’t we do more to help our 2D fellas out? Can we somehow pack more information into a 2D image to give them an even better understanding of a 3D object?</p>
      <p>This is where projection comes in.</p>
      <p>There are many types of projection, but the one we’ll be using is perspective projection. This type of projection is based on distance – the further a point is from the observer, the closer it will shrink towards the center of the projection image. This mimics what happens with our eyes, where objects appear to get smaller as they get further away.</p>
      <img class="img-wide lighter-image" src="~assets/perspective.png" alt="long hallway showing things that are further away being smaller">
      <p>So what would the perspective projection of a 3D cube into a 2D image look like?</p>
      <SceneButtonSingle :sceneID="scenes.threeandcanvas.projCube" :text="'LOAD SCENE'" :imgName="'proj_3dcube.png'"></SceneButtonSingle>
      <p>If this doesn’t seem that exciting, it’s because this 3D to 2D perspective projection is exactly how we’ve been representing 3D objects on this 2D website the entire time! 🤯 This output is equivalent to the 2D image one of our eyes would capture if we entered the scene, centered ourselves on the gray plane, then looked at the cube.</p>
      <p>We’re not done yet though – we can pack in even more information:</p>
      <SceneButtonSingle :sceneID="scenes.threeandcanvas.projEdgeCube" :text="'LOAD SCENE'" :imgName="'proj_3dcube_edge.png'"></SceneButtonSingle>
      <p>Now we can see all the edges of the cube at once! By observing how all the edges connect together, a 2D being could get a good idea of the cube’s overall structure. The only downside to perspective projection is angle distortion.</p>
      <p>To get a better view of this distortion, select “Highlight Face” in the current scene. You have to really force yourself to think in 2D for this one, but observe how the face's shape changes in the projection image during rotation. While a cube's actual face is always a square with 90° angles, the distorted angles can make the projection be a square, trapezoid, or any 4 sided shape in between depending on the cube’s orientation.</p>
      <img class="img-wide" src="~assets/proj_comparison.png" alt="square shown with 90 degree angle, cube projection shown with angle greater than 90">
      <p>So perspective projection won't always create a perfect representation of an object, but it’s still a very efficient way of compressing an object down a dimension.</p>
      <p>You can boost its effectiveness even further by highlighting an object's different points, edges, or faces to reveal different insights. Look at how without any highlights, the projection of a solid sphere doesn't appear to change during rotation:</p>
      <SceneButtonSingle :sceneID="scenes.threeandcanvas.projSphere" :text="'LOAD SCENE'" :imgName="'proj_3dsphere.png'"></SceneButtonSingle>
      <p>If instead we highlight points along the surface of the sphere, now we can observe how the surface moves during rotation:</p>
      <SceneButtonSingle :sceneID="scenes.threeandcanvas.projSpherePoints" :text="'LOAD SCENE'" :imgName="'proj_3dsphere_points.png'"></SceneButtonSingle>      
    </main>
  </div>
</template>

<script>
import {scenes} from '../scripts/constants'
import SceneButtonSingle from '../components/SceneButtonSingle'

let activeScene = undefined

export default {
  head: {
    title: 'Interactive 4D Handbook - 3D Projection',
    meta: [
      {
        hid: 'description',
        name: 'description',
        content: 'Interact with 3D spheres and cubes to see what their perspective projection to 2D looks like.'
      }
    ]
  },
  components: {
    SceneButtonSingle
  },
  data() {
    return {
      scenes: scenes,
    }
  },
  beforeMount() {
    if (!activeScene) {
      activeScene = scenes.threeandcanvas.projCube
    }
    this.$store.commit('updateScene', activeScene)
  },
  beforeDestroy() {
    activeScene = this.$store.state.sceneID
  }
}
</script>

<style scoped>
.lighter-image {
  border: solid 2px rgb(232, 232, 232);
}
</style>