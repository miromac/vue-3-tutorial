<template>
  <div>
    <div class="post" v-for="post in posts">
      <div><strong>Title:</strong> {{post.title}} </div>
      <div><strong>Description:</strong> {{post.body}} </div>
    </div>
</div>
</template>

<script>
export default {
  data() {
    return {
      posts: [
        { id: 1, title: 'Javascript', body: 'Javascript post description'},
        { id: 2, title: 'Angular', body: 'Angular post description'},
        { id: 3, title: 'React', body: 'React post description'},
        { id: 4, title: 'Vue', body: 'Vue post description'},
        { id: 5, title: 'Next', body: 'Next post description'}
      ]
    }
  },
  methods: {
    
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.post {
  margin: 15px;
  padding: 15px;
  border: 2px solid teal;
}
</style>

// Single file component
