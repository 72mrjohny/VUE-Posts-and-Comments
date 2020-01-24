<template>
  <div id="app">
    <section class="container">
      <PostsList />
    </section>
  </div>
</template>


<script>
import PostsList from "./components/PostsList.vue";

export default {
  components: {
    PostsList
  }
};
</script>
