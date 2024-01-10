<template>
    <div>
      <h1>Posts</h1>
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Title</th>
            <th>Body</th>
            <th>User ID</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="post in posts" :key="post.id">
            <td>{{ post.id }}</td>
            <td>{{ post.title }}</td>
            <td>{{ post.body }}</td>
            <td>{{ post.userId }}</td>
            <td>
              <button @click="viewComments(post.id)">View Comments</button>
            </td>
          </tr>
          <h2>Post Comments</h2>
          <ul v-for="comment in comments" :key="comment.id">
            <li>{{ comment.body }}</li>
          </ul>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  export default {
    data() {
      return {
        posts: [],
        comments:[],
      };
    },
    async mounted() {
      try {
        const response = await axios.get('https://dummyjson.com/posts');
        this.posts = response.data.posts;

      } catch (error) {
        console.error('Error fetching posts:', error);
      }
    },
    methods: {
      async viewComments(postId) {
        try {
          const response = await axios.get(
            `https://dummyjson.com/posts/${postId}/comments`
          );
          this.comments = response.data.comments;
        } catch (error) {
          console.error(`Error fetching comments for post ${postId}:`, error);
        }
      },
    },
  };
  </script>
  