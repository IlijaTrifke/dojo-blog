<template>
  <div v-if="error">{{ error }}</div>
  <div v-if="post" class="post">
    <h3>{{ post.title }}</h3>
    <p class="pre">{{ post.body }}</p>
    <button @click="handleClick" class="delete">Delete post</button>
  </div>
  <div v-else>
    <Spinner />
  </div>
</template>

<script>
import Spinner from "@/components/Spinner.vue";
import getPost from "../composables/getPost";
import { useRoute, useRouter } from "vue-router";

export default {
  props: ["id"],
  setup(props) {
    const route = useRoute();
    const router = useRouter();
    const uri = "http://localhost:3000/posts/" + props.id;

    const { post, error, load } = getPost(route.params.id); //ili prosto props.id
    load();

    const handleClick = async () => {
      await fetch(uri, {
        method: "DELETE",
      }).catch((error) => console.log(error.message));

      router.push({ name: "home" });
    };

    return { post, error, handleClick };
  },
  components: { Spinner },
};
</script>

<style>
.post {
  max-width: 1200px;
  margin: 0 auto;
}
.post p {
  color: #444;
  line-height: 1.5em;
  margin-top: 40px;
}
.pre {
  white-space: pre-wrap;
}
button.delete {
  margin: 10px auto;
}
</style>
