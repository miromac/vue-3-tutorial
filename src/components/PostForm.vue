<template>
  <form @submit.prevent>
    <h4>New post</h4>
    <input
      v-model="post.title"
      class="input"
      type="text"
      placeholder="Title"
    >
    <input
      v-model="post.body"
      class="input"
      type="text"
      placeholder="Description"
    >
    <button
      class="btn"
      @click="createPost"
    >
      Create
    </button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  createPost() {
      this.post.id = Date.now(),
      this.posts.push(newPost);
      this.title = '';
      this.body = '';
    }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}

.btn {
  margin-top: 15px;
  align-self: flex-end;
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 1px solid teal;
}
</style>
