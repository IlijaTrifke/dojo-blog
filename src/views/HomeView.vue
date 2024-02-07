<template>
  <div class="home">
    <h1>Home</h1>
    <div v-if="error">{{ error }}</div>
    <!-- v-if="showPosts"  -->
    <PostList v-if="posts.length" :posts="posts" />
    <div v-else>Loading...</div>
    <!-- <button @click="showPosts = !showPosts">toggle posts</button>
    <button @click="posts.pop()">delete a post</button> -->
  </div>
</template>

<script>
import PostList from "@/components/PostList.vue";
import getPosts from "../composables/getPosts";

export default {
  name: "HomeView",
  setup() {
    // const showPosts = ref(true);
    const { posts, error, load } = getPosts(); //imamo reference posts i error, tako da mu dodje isto samo smo olaksali sebi kod
    load();
    return {
      posts,
      //  showPosts
      error,
    };
  },
  components: { PostList },
};
</script>
