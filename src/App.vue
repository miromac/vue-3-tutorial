<template>
  <div class="app">
    <h1>Posts</h1>
    <my-button @click="fetchPosts"> Get axios posts</my-button>
    <my-button
      @click="showDialog"
      style="margin: 15px 0"
    >
      New post
    </my-button>
    <my-dialog v-model:show="dialogVisible">
      <post-form
      @create="createPost"
      />
    </my-dialog>
    <post-list
      :posts="posts"
      @remove="removePost"
    />
  </div>
</template>

<script>
import PostForm from '@/components/PostForm.vue';
import PostList from '@/components/PostList.vue';
import axios from 'axios';

export default {
  components: {
    PostList, PostForm
  },
  data() {
    return {
      posts: [
        { id: 1, title: 'Javascript', body: 'Javascript post description'},
        { id: 2, title: 'Angular', body: 'Angular post description'},
        { id: 3, title: 'React', body: 'React post description'},
        { id: 4, title: 'Vue', body: 'Vue post description'},
        { id: 5, title: 'Next', body: 'Next post description'}
      ],
      dialogVisible: false,
      modificatorValue: ''
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true;
    },
    async fetchPosts() {
      try {
        setTimeout( async () => {
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
          this.posts = response.data;
        }, 1000)
        
      } catch (e) {
        alert('Error')
      }
    }
  },
  mounted() {
    this.fetchPosts();
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}

</style>

// Single file component
