<template>
  <div v-theme:column="'narrow'" id="show-blogs">
    <h1>博客总览</h1>
    <input type="text" v-model="search" placeholder="搜索" />
    <div v-for="blog in filteredBlogs" class="single-blog" :key="blog.title">
      <router-link v-bind:to="'/blog/' + blog.id">
        <h2 v-rainbow>{{ blog.title }}</h2>
      </router-link>
      <article>{{ blog.content | snippet }}</article>
      <span>{{ blog.date }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "show-blogs",
  data() {
    return {
      blogs: [],
      search: ""
    };
  },
  created() {
    this.$http
      .get("https://myblogs-bda42.firebaseio.com/posts.json")
      .then(function(data) {
        //console.log(data.json());
        return data.json();
        // this.blogs = data.body.slice(0, 10);
        // console.log(this.blogs);
      })
      .then(function(data) {
        var blogsArray = [];
        for (let key in data) {
          // console.log(key);
          // console.log(data[key]);
          data[key].id = key;
          blogsArray.unshift(data[key]);
        }
        //console.log(blogsArray);
        this.blogs = blogsArray;
        console.log(this.blogs);
      });
  },
  computed: {
    filteredBlogs: function() {
      return this.blogs.filter(blog => {
        return blog.title.match(this.search);
      });
    }
  },
  filters: {
    "to-uppercase": function(value) {
      return value.toUpperCase();
      // toUpperCase(value) {
      //   return value.toUpperCase();
      // }
    }
  },
  directives: {
    rainbow: {
      bind(el, binding, vnode) {
        el.style.color =
          "#" +
          Math.random()
            .toString(16)
            .slice(2, 8);
      }
    }
  }
};
</script>

<style>
#show-blogs {
  max-width: 800px;
  margin: 0 auto;
}
.single-blog {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eeeeee;
  border: 1px dotted #aaaaaa;
}
#show-blogs a {
  color: #444;
  text-decoration: none;
}
input[type="text"] {
  padding: 8px;
  width: 100%;
  box-sizing: border-box;
}
span {
  float: right;
  margin-right: 30%;
  margin-top: 20px auto;
}
</style>
