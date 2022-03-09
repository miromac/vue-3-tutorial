<template>
  <div class="app">
    <post-form />
    <post-list />
  </div>
</template>

<script>
import PostForm from '@/components/PostForm.vue';
import PostList from '@/components/PostList.vue';

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
      title: '',
      body: ''
    }
  },
  methods: {
    createPost() {
      const newPost = {
        id: Date.now(),
        title: this.title,
        body: this.body,
      }
      this.posts.push(newPost);
      this.title = '';
      this.body = '';
    }
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
