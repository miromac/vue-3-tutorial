<template>
  <div>
    <h1>Posts</h1>
    <my-input
      v-model="searchQuery"
      placeholder="Search..."
      v-focus
    />
    <div class="app_btns">
      <my-button
      @click="showDialog"

      >
        New post
      </my-button>
      <my-select
        v-model="selectedSort"
        :options="sortOptions"
      />
    </div>
    <my-dialog v-model:show="dialogVisible">
      <post-form
      @create="createPost"
      />
    </my-dialog>
    <post-list
      :posts="sortedAndSearchedPosts"
      @remove="removePost"
      v-if="!isPostsLoading"
    />
    <div v-else>POSTS FROM jsonplaceholder.typicode.com ARE LOADING...</div>
    <div ref="observer" class="observer"></div>
  </div>
  <!-- <div class="page_wrapper">
    <div
      v-for="pageNumber in totalPages"
      :key="pageNumber"
      class="page"
      :class="{
        'current-page': page === pageNumber
      }"
      @click="changePage(pageNumber)"
    >
      {{ pageNumber }}
    </div>
  </div> -->
</template>

<script>
import PostForm from '@/components/PostForm.vue';
import PostList from '@/components/PostList.vue';
import axios from 'axios';
import MySelect from '@/components/UI/MySelect.vue';

export default {
  components: {
    PostList, PostForm, MySelect
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostsLoading: false,
      selectedSort: '',
      searchQuery: '',
      page: 1,
      limit: 10,
      totalPages: 0,
      sortOptions: [
        {value: 'title', name: 'By title'},
        {value: 'body', name: 'By content'},
      ]
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
    // changePage(pageNumber) {
    //   this.page = pageNumber;
    // },
    async fetchPosts() {
      try {
        this.isPostsLoading = true;
        setTimeout( async () => {
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
            params: {
              _page: this.page,
              _limit: this.limit
            }
          });
          this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
          this.posts = response.data;
        }, 1000)
        
      } catch (e) {
        alert('Error')
      } finally {
        this.isPostsLoading = false;
      }
    },
    async loadMorePosts() {
      try {
        this.page += 1;
        setTimeout( async () => {
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
            params: {
              _page: this.page,
              _limit: this.limit
            }
          });
          this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
          this.posts = [...this.posts, ...response.data];
        }, 1000)
        
      } catch (e) {
        alert('Error')
      } finally {
      }
    }
  },
  mounted() {
    this.fetchPosts();
    console.log(this.$refs.observer);
    let options = {
      rootMargin: '0px',
      threshold: 1.0
    }

    let callback = (entries, observer) => {
      if (entries[0].isIntersecting && this.page < this.totalPages) {
        this.loadMorePosts()
      }
    }

    let observer = new IntersectionObserver(callback, options);
    observer.observe(this.$refs.observer);
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort( (post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
    },
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
  },
  watch: {
    // page() {
    //   this.fetchPosts();
    // }
  }
}
</script>

<style>
.app_btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}
.page_wrapper {
  display: flex;
  margin-top: 10px;
}
.page {
  border: 1px solid black;
  padding: 10px;
}
.current-page {
  border: 2px solid teal;
}
.observer {
  height: 30px;
  background: green;
}
</style>

// Single file component
