<template>
  <div class="posts-list-wrapper">
    <div class="title">
      <h1>Lista artykułów</h1>
      <input type="text" v-model="search" placeholder="Wpisz tytuł " />
    </div>

    <div class="list-wrapper">
      <div
        v-for="(post,index) in posts"
        :key="index"
        v-show="filteredPostsIds.indexOf(index) > -1"
        :class="{'active': activeItemId === index}"
        @click="setActiveItemId(index)"
        class="post"
      >
        <PostCard :title="post.title" :text="post.body" :index="post.id" />
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
      activeItemId: "",
      search: ""
    };
  },
  methods: {
    setActiveItemId(index) {
      this.activeItemId = index;
      console.log(this.activeItemId);
    },
    fetchData: function() {
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
    this.fetchData();
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
<style scoped>
.title {
  position: relative;
  font-family: "Josefin Sans", sans-serif;
}
.title h1 {
  font-size: 30px;
  color: white;
  text-shadow: 2px 2px #000000;
  margin-left: 10vw;
}
.title input {
  background-color: #4b7cad;
  color: aliceblue;
  font-size: 20px;
  position: absolute;
  top: 10px;
  right: 10px;
  margin-right: 10vw;
  border: 2px solid rgb(255, 255, 255);
  padding: 4px;
}
::placeholder {
  color: rgb(255, 255, 255);
}
input:focus {
  box-shadow: 0px 0px 5px #ffffff;
}

.list-wrapper {
  display: inline-block;
  margin-left: 5vw;
  margin-right: 5vw;
  box-sizing: border-box;
  text-align: center;
}
.post {
  background-color: #2a4661;
  color: aliceblue;
  text-shadow: 2px 2px #000000;
  margin: 10px;
  padding: 10px;
  width: 90%;
  display: inline-block;
  transition: 0.3s;
  font-family: "Josefin Sans", sans-serif;
  border: 2px solid black;
  border-radius: 3px;
  box-sizing: border-box;
  text-align: left;
}
.post:hover {
  box-shadow: 0px 0px 13px #000000;
}
.post.active {
  background-color: #485f74;
}

/* SEKCJA MOBILE */

@media screen and (max-width: 800px) {
  .title h1 {
    margin-bottom: 60px;
  }
  .title input {
    margin-right: 8vw;
    top: 50px;
    font-size: 16px;
    padding: 2px;
  }
  .list-wrapper {
    margin-top: 10px;
  }
}
</style>


