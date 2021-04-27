<template>
  <div class="container">
    <h1>{{ msg }}</h1>
    <hr />
    <div class="form-todo form-group">
      <p>
        <input
          placeholder="Name"
          type="text"
          name="author"
          class="form-control"
          v-model="name"
        />
      </p>
      <p>
        <textarea
          placeholder="Message"
          name="message"
          class="form-control"
          v-model="message"
        ></textarea>
      </p>
      <button v-on:click="addComment" type="submit" class="btn btn-primary">
        Comment
      </button>
    </div>
    <hr />
    <div class="list-group">
      <p v-if="comments.length <=0"> No comments </p>
      <div
        class="list-group-item"
        v-for="(comment, index) in allComments"
        v-bind:key="index"
      >
        <span class="comment__author"
          >Autor: <strong>{{ comment.name }}</strong></span
        >
        <p>{{ comment.message }}</p>
        <div>
          <a v-on:click.prevent="removeComment(index)" href="#" title="Excluir"
            >Remove comment</a
          >
        </div>
      </div>
    </div>
    <hr />
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data: function () {
    return {
      comments: [],
      name: "",
      message: "",
    };
  },
  methods: {
    addComment() {
      if (this.message.trim() === "") return;

      this.comments.push({
        name: this.name,
        message: this.message,
      });

      this.name = "";
      this.message = "";
    },

    removeComment(index) {
      this.comments.splice(index, 1);
    },
  },
  computed: {
    allComments() {
      return this.comments.map((comment) => ({
        ...comment,
        name: comment.name.trim() === "" ? "Anonymous" : comment.name,
      }));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
