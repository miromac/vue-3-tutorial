<template>
  <div>
    <div class="post">
      <div><strong>Title:</strong> Post about JavaScript</div>
      <div><strong>Description:</strong> JavaScript, often abbreviated JS,
        is a programming language that is one of the core technologies of the World Wide Web,
        alongside HTML and CSS.</div>
    </div>
    <div class="post">
      <div><strong>Title:</strong> Post about JavaScript</div>
      <div><strong>Description:</strong> JavaScript, often abbreviated JS,
        is a programming language that is one of the core technologies of the World Wide Web,
        alongside HTML and CSS.</div>
    </div>
    <div class="post">
      <div><strong>Title:</strong> Post about JavaScript</div>
      <div><strong>Description:</strong> JavaScript, often abbreviated JS,
        is a programming language that is one of the core technologies of the World Wide Web,
        alongside HTML and CSS.</div>
    </div>
</div>
</template>

<script>
export default {
  data() {
    return {
      likes: 0,
      dislikes: 5,
    }
  },
  methods: {
    addLike() {
      this.likes += 1;
    },
    addDislike() {
      this.dislikes += 1;
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

.post {
  padding: 15px;
  border: 2px solid teal;
}
</style>

// Single file component
