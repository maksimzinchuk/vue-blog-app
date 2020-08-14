<template>
  <div>
    <ul class="comments-list">
      <Comment
        v-for="comment of post"
        v-bind:comment="comment"
        :key="comment.commentId"
        v-on:remove-comment="removeComment"
      />
    </ul>
  </div>
</template>

<script>
import Comment from "@/components/Comment.vue";
export default {
  props: ["post"],
  components: {
    Comment,
  },
  methods: {
    removeComment(id) {
      this.$emit("remove-comment", id);
    },
  },
};
</script>

<style lang="sass" scoped>
.comments-list
    list-style: none
    padding: 0
    margin-top: 20px
</style>
