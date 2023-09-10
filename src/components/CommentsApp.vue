<template>
  <div class="container">
    <h1>Commentaries</h1>
    <hr />
    <FormTodo v-on:add-todo="addComment"></FormTodo>
    <div class="list-group">
      <div class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="comment.id">
        <span class="comment__author">
          Author: <strong>{{ comment.name }}</strong></span
        >
        <p>{{ comment.message }}</p>
        <div>
          <a href="#" title="Delete" v-on:click.prevent="removeComment(index)"
            >Delete</a
          >
        </div>
      </div>
    </div>
    <hr />
  </div>
</template>

<script>
import FormTodo from './FormTodo.vue'
export default {
  components:{
    FormTodo
  },
  data() {
    return {
      comments: [],
    };
  },
  methods: {
    removeComment(index) {
      this.comments.splice(index, 1);
    },
    addComment(comment){
      this.comments.push(comment);

    }
  },
  computed: {
    allComments() {
      return this.comments.map((comment) => ({
        ...comment,
        name: comment.name.trim() === "" ? "Anonymous" : comment.name,
      }));
    },
  },
  watch: {
    comments(val) {
      console.log("val", val);
    },
  },
};
</script>
