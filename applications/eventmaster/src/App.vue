<template>
<div id="app">
  <h3>{{title}}</h3>
  <div class="post-button">
  <button class="btn btn-primary" @click="fetchPosts">Get your Posts</button>
  </div>
  <div class="col-md-12">
  <div class="col-md-4" v-for="(post,index) in posts" v-bind:key="post.id">
    <div class="post-card">
    <button class="close-button" @click="removePost(index)">&times;</button>
      <div class="card-block">
        <h4 class="card-title">{{post.title}}</h4>
        <p class="card-text">Description: {{post.body}}</p>
      </div>
    </div>
  </div>
  </div>
</div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios';
Vue.prototype.$http = axios;
import 'regenerator-runtime/runtime'

export default {
  name: 'app',
  data() {
    return {
      title: 'Generate Posts',
      posts: [],

    }
  },
  methods: {
  async fetchPosts() {
      try {
        const response = await this.$http.get(
        `http://jsonplaceholder.typicode.com/posts`
        );
        
        this.posts = response.data;
        console.log(this.posts);
      } catch (error) {
        console.log(error);
      }
    },
      removePost(index) {
        this.posts.splice(index, 1);
      }
  }
}
</script>
