<template>
  <div class="home">
    <h1>{{url}}</h1>
    <el-table
      :data="nodes"
      style="width: 100%"
      :row-class-name="tableRowClassName"
        :default-sort = "{prop: 'count', order: 'descending'}">
      <el-table-column
        prop="name"
        label="Name">
      </el-table-column>
      <el-table-column
        label="Version">
        <template slot-scope="scope">
          {{ scope.row.appName }} {{ scope.row.appVersion }}
        </template>
      </el-table-column>
      <el-table-column
        prop="count"
        label="Jobs"
        sortable>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      url: 'https://nutzdoch.einfachiota.de/nodes',
      nodes: []
    }
  },
  methods: {
    fetchData() {
      let self = this;
      fetch(this.url)
        .then(function(response) {
          return response.json();
        })
        .then(function(nodes) {
          console.log(nodes);
          if(nodes) {
            self.nodes = nodes
          }
        });
    },
    tableRowClassName({row}) {
        if (row.available && row.appName == 'POW Node') {
          return 'success-row';
        } 
        if (row.available && row.delay < 4) {
          return 'success-row';
        } 
        else {
          return 'danger-row';
        }
        return '';
      }
  },
  created() {
    this.fetchData();
  }
}
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
