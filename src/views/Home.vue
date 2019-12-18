<template>
  <div class="home">
    <div class="hero">
      <h1 class="heading">einfachIOTA Pool</h1>
      <p class="sub-heading">Der IOTA Node Pool der einfachIOTA community!</p>
    </div>
    
    <div class="section section-background">
      <div class="container">
        <h2>nutzdoch einfachIOTA!</h2>
        <p>Du kannst den einfachIOTA Pool in deiner Trinity Wallet als IOTA Node angeben und du hast zugriff auf alle Nodes im Pool!</p>
        <strong>Wähle einfach in der Trinity Node Liste diese URL aus:</strong>
        <el-alert
          title="URL erfolgreich kopiert!"
          type="success"
          center
          v-if="copied"
          class="el-zoom-in-top"
        ></el-alert>
        <h3 v-clipboard:copy="url" v-clipboard:success="onCopy" v-clipboard:error="onError">{{url}}</h3>
        <br>
        <button
          type="button"
          class="el-button el-button--primary"
          v-clipboard:copy="url"
          v-clipboard:success="onCopy"
          v-clipboard:error="onError"
        >URL Kopieren</button>
      </div>
    </div>
<div class="section">
      <div class="container">
        <h2>Was ist ein Pool?</h2>
        <p>Du möchtest mehr zum Pool und seine Funktionsweise erfahren? Klicke hier, um mehr darüber zu lesen.</p>
         <router-link
          to="/about"
          tag="button"
          class="el-button el-button--primary"
        >Entdecke den Pool</router-link>
      </div>
    </div>

<div class="section">
      <div class="container">
    <h2>Node Liste</h2>
    <NodeList/>
      </div>
    </div>
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
      setTimeout(
        function() {
          console.log("what?");
          this.copied = false;
        }.bind(this),
        1000
      );
    },
    onError() {
      console.log("copy error!");
    }
  }
};
</script>

<style lang="scss">
.el-main {
  padding: 0px !important;
}
.home {
  text-align: center;
}
.hero {
  margin: 0 10px;
}
.section {
  padding: 80px 0;
  &-background {
    background-color: var(--light);
    p {
      max-width: 600px;
      margin: 15px auto 30px;
    }
    a {
      text-decoration: none;
    }
  }

  .headline-wrapper {
    padding: 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
}
@media only screen and (max-width: 740px) {
  .hero {
    padding-top: 40px;
  }
  .headline-wrapper {
    flex-wrap: wrap;
    h2 {
      margin-bottom: 20px;
    }
  }
  .btn-social {
    margin-bottom: 5px !important;
  }
}
</style>