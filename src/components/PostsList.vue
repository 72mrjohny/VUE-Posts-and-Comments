<template>
  <div class="app-wrapper">
    <div class="title">
      <h1>Lista artykułów</h1>
      <input type="text" v-model="search" placeholder="Wpisz tytuł " />
    </div>

    <div class="list-wrapper">
      <div
        v-for="(post, index) in posts"
        :key="index"
        v-show="filteredPostsIds.indexOf(index) > -1"
        :class="{'active': activeItemId == post.id}"
        class="post"
      >
        <PostCard
          :post-id="post.id"
          :active-post-id="activeItemId"
          :title="post.title"
          :text="post.body"
          @commentButtonClick="setActiveItemId"
        />
      </div>
    </div>
  </div>
</template>

<script>
import PostCard from "./PostCard";

export default {
  name: "PostsList",
  components: {
    PostCard
  },
  data() {
    return {
      posts: [],
      activeItemId: null,
      search: ""
    };
  },
  methods: {
    setActiveItemId(index) {
      this.activeItemId = index;
    },
    getPost: function() {
      const myRequest = new Request(
        "https://jsonplaceholder.typicode.com/posts"
      );

      fetch(myRequest)
        .then(response => {
          return response.json();
        })
        .then(data => {
          this.posts = data;
        })
        .catch(error => {
          console.log(error);
        });
    }
  },

  mounted() {
    this.getPost();
  },
  computed: {
    filteredPostsIds: function() {
      var filteredIds = [];

      for (const [index, post] of this.posts.entries()) {
        if (
          this.search != "" &&
          !post.title.toLowerCase().match(this.search.toLowerCase())
        ) {
          continue;
        }

        filteredIds.push(index);
      }
      return filteredIds;
    }
  }
};
</script>



