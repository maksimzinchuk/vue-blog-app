<template>
  <div>
    <ul class="posts-list">
      <Post
        v-for="post of posts"
        v-bind:post="post"
        :key="post.post.id"
        v-on:remove-post="removePost"
        v-on:remove-comment="removeComment"
        v-on:add-comment="addComment"
        v-on:edit-post="editedPost"
      />
    </ul>
  </div>
</template>

<script>
import Post from "@/components/Post.vue";
export default {
  props: ["posts"],

  components: {
    Post,
  },
  methods: {
    removePost(id) {
      this.$emit("remove-post", id);
    },
    addComment(comment) {
      this.$emit("add-comment", comment);
    },
    removeComment(id) {
      this.$emit("remove-comment", id);
    },
    editedPost(post) {
      this.$emit("edit-post", post);
    },
  },
};
</script>

<style lang="sass" scoped>
.posts-list
    list-style: none
    width: 50%
    margin: 0 auto
</style>
