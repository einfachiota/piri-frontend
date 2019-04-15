<template>
  <div class="home">
    <h1>{{url}}</h1>
    <StatusBar />
    <NodeList />

  </div>
</template>

<script>
import StatusBar from './StatusBar'
import NodeList from './NodeList'

export default {
  name: "Home",
  components: { StatusBar, NodeList },
  data() {
    return {
      url: "https://nutzdoch.einfachiota.de/",
    }
  }
};
</script>