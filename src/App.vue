<template>
  <div class="container">
    <!-- Form -->
    <form @submit.prevent="save" class="form">
      <input type="text" v-model="form.title" placeholder="Title" class="input-field" /><br />
      <textarea v-model="form.content" placeholder="Content" class="input-field"></textarea><br />
      <button type="submit" class="button save-button">Save</button>
    </form>

    <!-- List of Articles -->
    <ul class="article-list">
      <li v-for="article in articles" :key="article.id" class="article-item">
        <h2 class="article-title">{{ article.title }}</h2>
        <p class="article-content">{{ article.content }}</p>
        <div class="button-container">
          <button @click="edit(article)" class="button edit-button">Edit</button>
          <button @click="deleteArticle(article.id)" class="button delete-button">Delete</button>
        </div>
      </li>
    </ul>

    <!-- Load Button -->
    <button @click="load" class="button load-button">Load</button>
  </div>
</template>

<script>
import { ref, reactive } from 'vue';

export default {
  setup() {
    const form = reactive({
      id: null,
      title: '',
      content: '',
    });

    const articles = ref([]);

    function load() {
      // Simulate loading articles locally
      articles.value = [
        { id: 1, title: 'Article A', content: 'Content of Article a' },
        { id: 2, title: 'Article B', content: 'Content of Article b' },
        { id: 3, title: 'Article C', content: 'Content of Article c' },
        { id: 1, title: 'Article D', content: 'Content of Article d' },
        { id: 2, title: 'Article E', content: 'Content of Article e' },
        { id: 3, title: 'Article F', content: 'Content of Article f' },
      ];
    }

    function save() {
      // Simulate saving article locally
      const newArticle = { id: form.id || articles.value.length + 1, title: form.title, content: form.content };
      if (form.id) {
        const index = articles.value.findIndex(article => article.id === form.id);
        if (index !== -1) {
          articles.value.splice(index, 1, newArticle);
        }
      } else {
        articles.value.push(newArticle);
      }

      // Reset form
      form.id = null;
      form.title = '';
      form.content = '';
    }

    function deleteArticle(id) {
      // Simulate deleting article locally
      articles.value = articles.value.filter(article => article.id !== id);
    }

    function edit(article) {
      form.id = article.id;
      form.title = article.title;
      form.content = article.content;
    }

    return { form, articles, save, edit, deleteArticle, load };
  },
};
</script>

<style>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.input-field {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.button {
  border: none;
  border-radius: 5px;
  padding: 10px px;
  cursor: pointer;
}

.save-button {
  background-color: #9157b4;
  color: white;
}

.load-button {
  background-color: #6b4060;
  color: white;
}

.edit-button {
  background-color: #d0ae7e;
  color: #333;
}

.delete-button {
  background-color: #9c7832;
  color: white;
}

.article-item {
  margin-bottom: 10px;
}

.article-title {
  font-size: 1.5em;
  margin-bottom: 5px;
}

.article-content {
  color: #555;
}

.button-container {
  display: flex;
  justify-content: space-between;
}
</style>