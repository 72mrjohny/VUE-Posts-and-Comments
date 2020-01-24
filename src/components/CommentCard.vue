<template>
  <div class="comment">
    <p class="comment--email">{{email}}</p>
    <p class="comment--description">{{body}}</p>
  </div>
</template>


<script>
export default {
  name: "CommentCard",

  props: {
    email: {
      type: String,
      default: "randomemail@gmail.com"
    },
    body: {
      type: String,
      default:
        "Lorem ipsum dolor sit amet consectetur adipisicing elit. Animi placeat quis deserunt architecto consectetur, repellendus deleniti laudantium, magnam odio laboriosam maiores magni corrupti debitis nostrum quibusdam distinctio beatae praesentium aperiam."
    }
  }
};
</script>

