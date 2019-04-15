<template>
  <div class="home">
    <h1>{{url}}</h1>
    <NodeList />
  </div>
</template>

<script>
import NodeList from './NodeList'
export default {
  name: "Home",
  components: { NodeList },
  data() {
    return {
      url: "https://nutzdoch.einfachiota.de/",
    }
  }
};
</script>