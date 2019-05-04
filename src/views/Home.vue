<template>
  <div class="home">
    <h1>einfachIOTA Pool</h1>
    <el-alert
        title="success alert"
        type="success"
        center
        v-if="copied"
        class="el-zoom-in-top">
      </el-alert>
    <h3 v-clipboard:copy="url" v-clipboard:success="onCopy" v-clipboard:error="onError">{{url}}</h3>
    <button
      type="button"
      class="el-button el-button--primary"
      v-clipboard:copy="url"
      v-clipboard:success="onCopy"
      v-clipboard:error="onError"
    >Kopieren</button>
    <h2>Pool Status</h2>
    <StatusBar/>
    <h2>Node Liste</h2>
    <NodeList/>
  </div>
</template>

<script>
import StatusBar from "../components/StatusBar";
import NodeList from "../components/NodeList";

export default {
  name: "Home",
  components: { StatusBar, NodeList },
  data() {
    return {
      copied: false,
      url: "https://nutzdoch.einfachiota.de"
    };
  },
  methods: {
    onCopy() {
      this.copied = true;
      console.log("copy success!");
      setTimeout(function () {
        console.log("what?")
        this.copied = false;
      }.bind(this), 1000);
    },
    onError() {
      console.log("copy error!");
    }
  }
};
</script>