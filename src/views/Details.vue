<template>
  <div class="detail">
    <h3>Node Details</h3>
    <NodeDetails :node="$route.params.nodeId"/>
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