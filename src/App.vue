<template>
  <div id="app">
    <blog-header></blog-header>
    <!-- <add-blog></add-blog> -->
    <!-- <show-blogs></show-blogs> -->
    <router-view></router-view>
  </div>
</template>

<script>
import AddBlog from "./components/AddBlog";
import ShowBlogs from "./components/ShowBlogs";
import BlogHeader from "./components/BlogHeader";
export default {
  name: "App",
  components: {
    AddBlog,
    ShowBlogs,
    BlogHeader
  }
};
</script>

<style></style>
