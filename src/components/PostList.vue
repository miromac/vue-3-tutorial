<template>
  <div class="post" v-for="post in posts">
      <div><strong>Title:</strong> {{post.title}} </div>
      <div><strong>Description:</strong> {{post.body}} </div>
    </div>
</template>

<script>
export default {

}
</script>

<style scoped>
.post {
  margin: 15px;
  padding: 15px;
  border: 2px solid teal;
}
</style>
