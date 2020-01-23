<template>
  <div class="wrapper">
    <h1 class="post--title">{{title}}</h1>
    <p class="post--description">{{text}}</p>
    <div
      v-for="(comment,index) in comments"
      :key="index"
      v-show="comment.postId === 1"
      class="comment"
    >
      <p class="comment--email">{{comment.email}}</p>
      <p class="comment--description">{{comment.body}}</p>
    </div>

    <button class="btn" @click="getComments" v-if="!additionalPostStatus">Komentarze</button>
  </div>
</template>


<script>
export default {
  name: "PostCard",
  data() {
    return {
      comments: [],
      additionalPostStatus: false
    };
  },
  props: {
    title: {
      type: String,
      default: "Tytuł Artykułu"
    },
    text: {
      type: String,
      default:
        "Lorem ipsum dolor sit amet consectetur adipisicing elit. Animi placeat quis deserunt architecto consectetur, repellendus deleniti laudantium, magnam odio laboriosam maiores magni corrupti debitis nostrum quibusdam distinctio beatae praesentium aperiam."
    },
    index: {
      type: Number,
      default: 0
    }
  },

  methods: {
    getComments: function() {
      const myRequest = new Request(
        "https://jsonplaceholder.typicode.com/comments"
      );

      fetch(myRequest)
        .then(response => {
          return response.json();
        })
        .then(data => {
          this.comments = data;
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

<style scoped>
.post--title::first-letter,
.post--description::first-letter {
  text-transform: uppercase;
}
.comment {
  font-family: "Signika", sans-serif;
  background-color: #feffa8;
  color: #000000;
  padding-left: 20px;
  padding-right: 10px;
  margin: 3px;
  text-shadow: none;
  border: 1px solid rgb(8, 8, 8);
}
.comment--email {
  text-align: right;
  font-size: 1.2rem;
}
.comment--description {
  font-size: 0.9rem;
}
.btn {
  text-transform: uppercase;
  font-family: "Signika", sans-serif;
  letter-spacing: 1px;
  padding: 4px;
  cursor: pointer;
  background-color: #426091e3;
  color: #000000;
  border: 1px solid rgb(0, 0, 0);
  transition: 0.3s;
}
.active .wrapper .btn {
  background-color: #688dc9e3;
}

.btn:hover {
  text-shadow: 0px 0px 1px rgba(0, 0, 0, 0.932);
  color: #ffffff;
  border-color: white;
  box-shadow: 0 0 4px rgb(255, 255, 255);
}
</style>
