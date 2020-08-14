<template>
  <div>
    <h2>Добавить новый пост</h2>

    <form action="" class="new-post" v-on:submit.prevent="addPost">
      <input
        class="new-post__title"
        type="text"
        placeholder="заголовок поста"
        v-model="title"
        required
      />
      <textarea
        class="new-post__short"
        cols="30"
        rows="2"
        placeholder="короткое описание"
        v-model="shortPost"
        required
      ></textarea>
      <textarea
        class="new-post__full"
        cols="30"
        rows="10"
        placeholder="полное описание"
        v-model="fullPost"
        required
      ></textarea>
      <button class="new-post__send" type="submit">Создать пост</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      shortPost: "",
      fullPost: "",
    };
  },
  methods: {
    addPost() {
      const newPost = {
        post: {
          id: Date.now(),
          title: this.title,
          shortPost: this.shortPost,
          fullPost: this.fullPost,
        },
        comments: [],
      };

      this.$emit("add-post", newPost);
      this.title = "";
      this.shortPost = "";
      this.fullPost = "";
    },
  },
};
</script>

<style lang="sass" scoped>
.new-post
    display: flex
    flex-direction: column
    width: 400px
    margin: 0 auto

.new-post__short
    margin-top: 10px

.new-post__full
    margin-top: 10px

.new-post__send
    margin-top: 10px
    outline: none
</style>
