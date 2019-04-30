<template>
  <div>{{node}}</div>
</template>

<script>
export default {
  name: "NodeDetails",
  props: ["node"],
  data() {
    return {
      loading: false,
      url: "https://score.api.einfachiota.de"
    };
  },
  methods: {
    fetchData() {
      let self = this;
      fetch(this.url)
        .then(function(response) {
          return response.json();
        })
        .then(function(nodes) {
          if (nodes) {
            self.nodes = nodes;
            self.loading = false;
          }
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

