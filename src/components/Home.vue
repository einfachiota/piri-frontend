<template>
  <div class="home" v-loading="loading">
    <h1>{{url}}</h1>
    <el-table
      :data="nodes"
      style="width: 100%"
      :row-class-name="tableRowClassName"
      :default-sort="{prop: 'count', order: 'descending'}"
    >
      <el-table-column prop="name" label="Name"></el-table-column>
      <el-table-column label="Version">
        <template slot-scope="scope">{{ scope.row.appName }} {{ scope.row.appVersion }}</template>
      </el-table-column>
      <el-table-column prop="count" label="Jobs" sortable></el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      loading: false,
      url: "https://nutzdoch.einfachiota.de/nodes",
      nodes: []
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
    },
    tableRowClassName({ row }) {
      if (row.available && row.appName == "POW Node" || row.available && row.delay < 4) {
        return "success-row";
      } else {
        return "danger-row";
      }
    }
  },
  created() {
    this.loading = true;
    this.fetchData();
    this.intervalid1 = setInterval(
      function() {
        console.log("s")
        this.fetchData();
      }.bind(this),
      5000
    );
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.el-table .danger-row {
  background: #ffb3b3;
}

.el-table .success-row {
  background: #b3ffb3;
}
</style>
