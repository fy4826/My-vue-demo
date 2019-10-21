<template>
  <div>
    <Header></Header>
    <users></users>
    <Footer></Footer>
  </div>
</template>

<script>
import Header from "./components/Header";
import Users from "./components/Users";
import Footer from "./components/Footer";

export default {
  name: "app",
  data() {
    return {
      title: "第一个Vue脚手架项目"
    };
  },
  components: {
    Header,
    "users":Users,
    Footer
  }
};
</script>

<style>
</style>
