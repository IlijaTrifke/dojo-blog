<template>
  <div class="home">
    <h1>Home</h1>
    <div v-if="error">{{ error }}</div>
    <!-- v-if="showPosts"  -->
    <div v-if="posts.length" class="layout">
      <PostList v-if="posts.length" :posts="posts" />
      <TagCloud :posts="posts" />
    </div>
    <div v-else>
      <Spinner />
    </div>
    <!-- <button @click="showPosts = !showPosts">toggle posts</button>
    <button @click="posts.pop()">delete a post</button> -->
  </div>
</template>

<script>
import PostList from "@/components/PostList.vue";
import getPosts from "../composables/getPosts";
import Spinner from "@/components/Spinner.vue";
import TagCloud from "@/components/TagCloud.vue";

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
  components: { PostList, Spinner, TagCloud },
};
</script>

<style>
.home {
  max-width: 1200px;
  margin: 0 auto;
  padding: 10px;
}
.layout {
  display: grid;
  grid-template-columns: 3fr 1fr;
  gap: 20px;
}
</style>
