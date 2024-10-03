<template>
    <div class="post">
      <h3 v-html="highlightedTitle"></h3>
      <p v-html="highlightedContent"></p>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      title: {
        type: String,
        required: true
      },
      content: {
        type: String,
        required: true
      },
      searchQuery: {
        type: String,
        default: ''
      }
    },
    computed: {
      highlightedTitle() {
        return this.highlightText(this.title);
      },
      highlightedContent() {
        return this.highlightText(this.content);
      }
    },
    methods: {
      highlightText(text) {
        if (!this.searchQuery) return text;
        const regex = new RegExp(`(${this.searchQuery})`, 'gi');
        return text.replace(regex, '<mark>$1</mark>');
      }
    }
  };
  </script>
  
  <style scoped>
  .post {
    margin: 20px 0;
  }
  
  mark {
    background-color: yellow;
  }
  </style>
  