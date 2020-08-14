<template>
  <div class="home">
    <div>
      <NewPost v-on:add-post="addPost" />
      <h2 v-if="posts.length">Список постов</h2>
      <p class="no-posts" v-else>Постов пока что нет :(</p>
      <AllPosts
        v-bind:posts="posts"
        v-on:remove-post="removePost"
        v-on:add-comment="addComment"
        v-on:remove-comment="removeComment"
        v-on:edit-post="editPost"
      />
    </div>
  </div>
</template>

<script>
import NewPost from "@/components/NewPost.vue";
import AllPosts from "@/components/AllPosts.vue";
export default {
  name: "Home",
  data() {
    return {
      posts: [],
      comments: [],
    };
  },
  components: {
    NewPost,
    AllPosts,
  },
  methods: {
    addPost(newPost) {
      this.posts.unshift(newPost);
    },
    editPost(post) {
      const findIndex = this.posts.findIndex((x) => x.post.id == post.post.id);

      this.posts.splice(findIndex, 1, post);
    },
    removePost(id) {
      this.posts = this.posts.filter((item) => item.post.id !== id);
    },
    removeComment(id) {
      let newArr = [];
      this.posts.forEach((post) => {
        const findIndex = post.comments.findIndex(
          (comment) => comment.commentId == id
        );

        if (findIndex >= 0) {
          post.comments.splice(findIndex, 1);
        }
        newArr.push(post);

        this.posts = newArr;
      });
    },
    addComment(comments) {
      this.comments.push(comments);

      const foundIndex = this.posts.findIndex(
        (post) => post.id == comments.postid
      );

      this.posts[foundIndex] = comments;

      return;
    },
  },

  mounted() {
    if (localStorage.getItem("posts")) {
      this.posts = JSON.parse(localStorage.getItem("posts"));
    }
  },
  watch: {
    posts: {
      handler() {
        localStorage.setItem("posts", JSON.stringify(this.posts));
      },
    },
    comments: {
      handler() {
        localStorage.setItem("posts", JSON.stringify(this.posts));
      },
    },
  },
};
</script>

<style lang="sass">
.no-posts
  margin-top: 50px
</style>
