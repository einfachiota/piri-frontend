<template>
  <div class="detail">
    <h3>Node Details</h3>
    <NodeDetails :nodeName="$route.params.nodeName"/>
  </div>
</template>

<script>
import NodeDetails from '../components/NodeDetails'

export default {
  name: "Details",
  components: { NodeDetails },
  data() {
    return {
      url: "https://nutzdoch.einfachiota.de/",
    }
  }
};
</script>