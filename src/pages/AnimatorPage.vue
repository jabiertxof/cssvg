<template>
  <iframe id="broadway" style="width:100%;border:none;height:75vh" src="http://127.0.0.1:8085" />
  <q-page style="height: 25vh;" v-if="mount">
    <div id="page">
      <anim-editor />
      <anim-viewer />
    </div>
  </q-page>
  <h3 v-else style="text-align:Center">loading...</h3>
</template>

<script setup lang="ts">
import AnimEditor from "src/components/AnimEditor/AnimEditor.vue";
import { svgIO } from "src/modules/svgIO_m";
import { onBeforeMount, ref } from "vue";
import { useRoute } from "vue-router";
import AnimViewer from "../components/AnimViewer.vue";
const route = useRoute()
const mount = ref(!route.query.refreshApp)
onBeforeMount(() => {
  if (route.query.refreshApp) { location.replace(''); return }
  svgIO.input()
})

</script>

<style scoped>
#page {
  display: grid;
  grid-template-columns: 70% auto;
  gap: 3px;
  margin-top:20px;
  /* overflow: visible; */
  height: inherit;
}
</style>
