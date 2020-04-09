<template>
  <div id="add-blog">
    <span
      >{{ new Date().toLocaleDateString() }}--{{ new Date().getHours() }} :
      {{ new Date().getMinutes() }}记事</span
    >
    <hr />
    <h2>添加博客</h2>
    <form v-if="!submitted">
      <label>博客标题</label>
      <input type="text" v-model="blog.title" required />
      <label>博客内容</label>
      <textarea v-model="blog.content"></textarea>
      <div id="checkboxes">
        <label>vue.js</label>
        <input type="checkbox" value="vue.js" v-model="blog.categories" />
        <label>node.js</label>
        <input type="checkbox" value="node.js" v-model="blog.categories" />
        <label>react.js</label>
        <input type="checkbox" value="react.js" v-model="blog.categories" />
        <label>angular4</label>
        <input type="checkbox" value="angular4" v-model="blog.categories" />
      </div>
      <label>作者</label>
      <select v-model="blog.author">
        <option v-for="author in authors" :key="author">{{ author }}</option>
      </select>
      <button v-on:click.prevent="post">添加博客</button>
    </form>
    <div v-if="submitted">
      <h3>您的博客发布成功</h3>
    </div>
    <hr />
    <div id="preview">
      <h3>博客总览</h3>
      <p>博客标题：{{ blog.title }}</p>
      <p>博客内容：</p>
      <p>{{ blog.content }}</p>
      <p>博客分类：</p>
      <ul>
        <li v-for="category in blog.categories" :key="category.name">
          {{ category }}
        </li>
      </ul>
      <p>作者：{{ blog.author }}</p>
      <p>时间：{{ blog.date }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "add-blog",
  data() {
    return {
      blog: {
        title: "",
        content: "",
        categories: [],
        author: "",
        date:
          new Date().toLocaleDateString() +
          "--" +
          new Date().getHours() +
          ":" +
          new Date().getMinutes()
        // "new Date().toLocaleDateString()" +
        // "new Date().getHours()" +
        // "new Date().getMinutes() "
      },
      authors: ["lvan", "tony", "telly"],
      submitted: false
    };
  },
  methods: {
    post: function() {
      this.$http
        .post("https://myblogs-bda42.firebaseio.com/posts.json", this.blog)
        .then(function(data) {
          console.log(data);
          this.submitted = true;
        });
    }
  }
};
</script>

<style scoped>
#add-blog * {
  box-sizing: border-box;
}
#add-blog {
  margin: 20px auto;
  max-width: 600px;
  padding: 20px;
}
span {
  display: block;
  height: 20px;
  text-align: center;
  color: #555;
}
label {
  display: block;
  margin: 20px 0 10px;
}
input[type="text"],
textarea,
select {
  display: block;
  width: 100%;
  padding: 8px;
}
textarea {
  height: 200px;
}
#checkboxes label {
  display: inline-block;
  margin-top: 0;
}
#checkboxes input {
  display: inline-block;
  margin-right: 10px;
}
button {
  display: block;
  margin: 20px 0;
  background: #cccccc;
  color: crimson;
  border: 0;
  padding: 14px;
  border-radius: 4px;
  font-size: 18px;
  cursor: pointer;
}
#preview {
  padding: 10px 20px;
  border: 1px dotted #cccccc;
  margin: 30px 0;
}
h3 {
  margin-top: 10px;
}
</style>
