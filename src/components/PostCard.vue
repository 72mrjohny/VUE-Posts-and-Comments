<template>
  <div class="wrapper">
    <h1 class="post--title">{{title}}</h1>
    <p class="post--description">{{text}}</p>

    <div v-for="(comment,index) in comments" :key="index" v-show="postId === activePostId">
      <CommentCard :email="comment.email" :body="comment.body" />
    </div>

    <button class="btn" @click="getComments" v-if="postId != activePostId">Komentarze</button>
  </div>
</template>


<script>
import CommentCard from "./CommentCard";
export default {
  name: "PostCard",
  components: {
    CommentCard
  },
  data() {
    return {
      comments: []
    };
  },
  props: {
    postId: {
      type: Number,
      required: true
    },
    activePostId: {
      type: Number,
      default: null
    },
    title: {
      type: String,
      default: "Tytuł Artykułu"
    },
    text: {
      type: String,
      default:
        "Lorem ipsum dolor sit amet consectetur adipisicing elit. Animi placeat quis deserunt architecto consectetur, repellendus deleniti laudantium, magnam odio laboriosam maiores magni corrupti debitis nostrum quibusdam distinctio beatae praesentium aperiam."
    }
  },

  methods: {
    getComments: function() {
      const myRequest = new Request(
        `https://jsonplaceholder.typicode.com/comments?postId=${this.postId}`
      );

      fetch(myRequest)
        .then(response => {
          return response.json();
        })
        .then(data => {
          this.$emit("commentButtonClick", this.postId);
          this.comments = data;
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>


