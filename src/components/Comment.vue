<template>
  <div>
    <li>
      <section class="comment">
        <div class="comment__user-wrapper">
          <div class="comment__image"></div>
          <h2 class="comment__username">{{ comment.name }}</h2>
        </div>
        <div class="comment__wrapper">
          <p class="comment__comment">{{ comment.comment }}</p>
        </div>
        <button
          class="comment__remove"
          v-on:click="$emit('remove-comment', comment.commentId)"
        >
          Удалить
        </button>
      </section>
    </li>
  </div>
</template>

<script>
export default {
  props: ["comment"],
};
</script>

<style lang="sass" scoped>
.comment
  border: 1px solid black
  border-radius: 5px
  width: 80%
  margin: 10px auto
  display: flex
  flex-direction: row

.comment__user-wrapper
  width: 20%

.comment__wrapper
  width: 80%

.comment__comment
  text-align: start
  margin: 10px

.comment__image
  background-image: url('./../assets/default-user-image.png')
  background-size: 100px 100px
  height: 100px
  width: 100px
  background-repeat: no-repeat
  margin: 5px auto

.comment__username
  font-size: 20px
  text-overflow: ellipsis
  overflow: hidden
  margin: 10px

.comment__remove
  align-self: flex-end
  margin: 10px
</style>
