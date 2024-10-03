<template>
  <div id="app" class="container">
    <div class="search-box">
      <input 
        v-model="searchQuery" 
        placeholder="Search..." 
        @input="onInput"
      />
      <button v-if="searchQuery" class="clear-btn" @click="clearSearch">×</button>
    </div>
    <p>{{ filteredPosts.length }} posts were found.</p>

    <Article
      v-for="post in filteredPosts"
      :key="post.id"
      :title="post.title"
      :content="post.content"
      :searchQuery="searchQuery"
    />
  </div>
</template>

<script>
import Article from './components/Article.vue';

export default {
  components: {
    Article
  },
  data() {
    return {
      searchQuery: '',
      articles: [
        {
          id: 1,
          title: "Understanding the difference between grid-template and grid-auto",
          content: "With all the new properties related to CSS Grid Layout, one of the distinctions that always confused me was the difference between the grid-template-* and grid-auto-* properties..."
        },
        {
          id: 2,
          title: "Recreating the GitHub Contribution Graph with CSS Grid",
          content: "In this post, I will walk you through how to recreate GitHub's contribution graph using CSS Grid..."
        }
        // Add more articles as necessary
      ]
    };
  },
  computed: {
    filteredPosts() {
      const query = this.searchQuery.toLowerCase();
      return this.articles.filter(article =>
        article.title.toLowerCase().includes(query) ||
        article.content.toLowerCase().includes(query)
      );
    }
  },
  methods: {
    clearSearch() {
      this.searchQuery = '';
    },
    onInput() {
      // Any additional handling for input events can be done here
    }
  }
};
</script>

<style>
.container {
  background-color: #f0f0f0;
  padding: 40px;
  min-height: 100vh;
  font-family: Arial, sans-serif;
}

.search-box {
  position: relative;
  margin-bottom: 20px;
}

input {
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.clear-btn {
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  border: none;
  background: transparent;
  font-size: 20px;
  cursor: pointer;
  color: #888;
}

.clear-btn:hover {
  color: #333;
}

p {
  margin-bottom: 20px;
  font-size: 16px;
  color: #333;
}

mark {
  background-color: #f5e12b;
  padding: 2px 4px;
}
</style>
