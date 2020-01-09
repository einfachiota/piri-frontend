<template>
  <div>
    <h1>{{nodeName}}</h1>
    <pre>{{details}}</pre>
  </div>
</template>

<script>
export default {
  name: "NodeDetails",
  props: ["nodeName"],
  data() {
    return {
      loading: false,
      url: "https://scoreapi.tanglebay.org/nodes",
      details: {},
      intervalid1: null
    };
  },
  methods: {
    fetchData() {
      let self = this;
      fetch(this.url + this.nodeName)
        .then(function(response) {
          return response.json();
        })
        .then(function(response) {
          console.log("what", response)
          self.details = response;
        });
    }
  },
  mounted() {
    console.log("details")

    this.loading = true;
    this.fetchData();
    this.intervalid1 = setInterval(
      function() {
        this.fetchData();
      }.bind(this),
      5000
    );
  },
  beforeDestroy () {
    clearInterval(this.intervalid1)
  }
};
</script>

