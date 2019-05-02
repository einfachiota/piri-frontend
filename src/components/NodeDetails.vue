<template>
  <div>{{nodeName}}</div>
</template>

<script>
export default {
  name: "NodeDetails",
  props: ["nodeName"],
  data() {
    return {
      loading: false,
      url: "https://pool.einfachiota.de/nodes/"
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
        });
    }
  },
  created() {
    this.loading = true;
    this.fetchData();
    this.intervalid1 = setInterval(
      function() {
        this.fetchData();
      }.bind(this),
      5000
    );
  }
};
</script>

