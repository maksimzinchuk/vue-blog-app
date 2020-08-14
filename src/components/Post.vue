<template>
  <div>
    <li>
      <div class="post">
        <button v-on:click="$emit('remove-post', post.post.id)">
          Удалить пост
        </button>
        <div
          class="post__wrapper"
          @click="showFull = !showFull"
          v-show="!postEdit"
        >
          <h2 class="post__header">{{ post.post.title }}</h2>
          <p class="post__short">{{ post.post.shortPost }}</p>
          <p v-show="!showFull">Комментариев: {{ commentsNumber }}</p>
        </div>

        <div v-show="showFull">
          <article class="post__full" v-show="!postEdit">
            {{ post.post.fullPost }}
          </article>

          <form
            class="post__edit"
            v-show="postEdit"
            v-on:submit.prevent="editPost"
          >
            <input v-model="post.post.title" />
            <input v-model="post.post.shortPost" />
            <textarea
              cols="30"
              rows="10"
              v-model="post.post.fullPost"
            ></textarea>

            <button
              type="submit"
              v-show="postEdit"
              @click="postEdit = !postEdit"
            >
              Отредактировать
            </button>
          </form>

          <button @click="postEdit = !postEdit" class="post__edit-button">
            Редактировать пост
          </button>

          <form class="comment-add" v-on:submit.prevent="addComment">
            <input
              type="text"
              name=""
              id=""
              placeholder="Имя комментатора"
              class="comment-add__name"
              v-model="name"
              required
            />
            <textarea
              name=""
              id=""
              cols="30"
              rows="5"
              placeholder="текст комментария"
              class="comment-add__comment"
              v-model="comment"
              required
            ></textarea>
            <button class="comment-add__button" type="submit">
              Добавить комментарий
            </button>
          </form>

          <AllComments
            v-bind:post="post.comments"
            v-on:remove-comment="removeComment"
          />
        </div>
      </div>
    </li>
  </div>
</template>

<script>
import AllComments from "@/components/AllComments.vue";
export default {
  props: {
    post: {
      type: Object,
    },
  },
  data() {
    return {
      showFull: false,
      postEdit: false,
      name: "",
      comment: "",
    };
  },
  computed: {
    commentsNumber() {
      return this.post.comments.length;
    },
  },
  components: {
    AllComments,
  },
  methods: {
    editPost() {
      const editedPost = this.post;

      this.$emit("edit-post", editedPost);
    },
    addComment() {
      const newComment = {
        postid: this.post.post.id,
        commentId: Date.now(),
        name: this.name,
        comment: this.comment,
      };

      this.post.comments.push(newComment);

      this.$emit("add-comment", this.post);

      this.name = "";
      this.comment = "";
    },
    removeComment(id) {
      this.$emit("remove-comment", id);
    },
  },
};
</script>

<style lang="sass" scoped>
.post
    border: 1px solid black
    border-radius: 5px
    margin-bottom: 10px


.post__header
    background-color: #c2c2c2
    margin: 0
    max-height: 100px
    font-size: 30px


.post__short
    background-color: #e0dada
    margin: 0
    font-size: 20px

.post__full
    margin: 20px
    border: 1px solid black
    height: 100px
    background-color: #E0DDDD
    font-size: 20px

.comment-add
    display: flex
    flex-direction: column
    width: 80%
    margin: 0 auto

.comment-add__comment
    margin-top: 10px

.comment-add__button
    margin-top: 10px

.post__edit
  display: flex
  flex-direction: column
  width: 80%
  margin: 0 auto


.post__edit-button
  margin: 10px
  background-color: #ff7367
  box-shadow: 0 1px 1px black
  outline: none
</style>
