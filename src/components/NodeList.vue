<template>
  <el-table
    v-loading="loading"
    :data="nodes"
    style="width: 100%"
    :row-class-name="tableRowClassName"
    :default-sort="{prop: 'score', order: 'descending'}"
    @row-click="rowClicked"
  >
    <el-table-column prop="name" label="Name"></el-table-column>
    <el-table-column label="Version">
      <template slot-scope="scope">{{ scope.row.appName }} {{ scope.row.appVersion }}</template>
    </el-table-column>
    <el-table-column prop="score" label="Score" sortable></el-table-column>
  </el-table>
</template>

<script>
export default {
  name: "NodeList",
  data() {
    return {
      loading: false,
      url: "https://score.api.einfachiota.de",
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
      if (
        (row.available && row.appName == "POW Node") ||
        (row.available && row.delay < 4)
      ) {
        return "success-row";
      } else {
        return "danger-row";
      }
    },
    rowClicked(row) {
      console.log("row", row)
      this.$router.push({ name: 'details', params: { nodeName: row.name } })
        console.log("row2")

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

<style>

.el-table .el-table__row {
  cursor: pointer;
}

.el-table .danger-row {
  background: #ffb3b3;
}

.el-table .success-row {
  background: #b3ffb3;
}
</style>

