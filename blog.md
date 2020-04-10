# 实现post数据

网址：jsonplaceholder

```js
post: function() {
      this.$http
        .post("http://jsonplaceholder.typicode.com/posts", {
          title:this,blog.title,
          body:this.blog.content,
          userId:1
      })
        .then(function(data) {             //.then就是请求数据成功之后要做的事情
          console.log(data);
          this.submitted = true;
        });
    }
```

# 自定义指令

## 钩子函数

参数：el、binding、vnode

## 自定义一个指令

位置：全局的在main.js中定义

```js
Vue.directive("rainbow", {
   bind(el, binding, vnode) {
    el.style.color =
      "#" +
       Math.random()
        .toString(16)
        .slice(2, 8);
   }
 });
```

如果不是全局的，就要在script标签中定义,在directives属性中

```js
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
```

# 过滤器  filter

同样，全局的在main.js中定义

```js
//自定义过滤器
// Vue.filter("to-uppercase", function(value) {
//   return value.toUpperCase();
// });
Vue.filter("snippet", function(value) {
  return value.slice(0, 100) + "...";
});
```

不是全局的就要在script中定义

```js
filters: {
    "to-uppercase": function(value) {
      return value.toUpperCase();
      // toUpperCase(value) {
      //   return value.toUpperCase();
      // }
    }
  },
```



## 搜索框的实现

计算属性   对于任何复杂逻辑，你都应当使用**计算属性**

```js
computed: {
    filteredBlogs: function() {
      return this.blogs.filter(blog => {
        return blog.title.match(this.search);
      });
    }
  },
```

# 路由

创建路由

```js
const router = new VueRouter({
  routes: Routes,           //单写一个路由的页面
  mode: "history"
});
```

```js
import AddBlog from "./components/AddBlog.vue";
import ShowBlogs from "./components/ShowBlogs.vue";
import SingleBlog from "./components/SingleBlog.vue";
export default [
  { path: "/", component: ShowBlogs },
  { path: "/add", component: AddBlog },
  { path: "/blog/:id", component: SingleBlog }
];

```

路由参数

