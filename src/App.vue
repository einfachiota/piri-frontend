<template>
  <div id="app">
    <div id="nav">
      <el-row>
        <el-col :span="24">
          <el-menu theme="dark" default-active="1" class="el-menu-demo" mode="horizontal">
            <el-menu-item index="1">
              <router-link to="/" class="link-item">Home</router-link>
            </el-menu-item>
            <el-menu-item index="2">
              <router-link to="/about" class="link-item">About</router-link>
            </el-menu-item>
          </el-menu>
        </el-col>
      </el-row>
    </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.logo {
  height: 200px;
}

.el-menu-item {
  overflow: hidden;
  position: relative;
  min-width: 100px;
}
.link-item {
  height: 100%;
  width: 100%;
  position: absolute;
  right: 0;
  top: 0;
  text-decoration: none;
}
</style>
