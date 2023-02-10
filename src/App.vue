<script setup>
import PaginatePost from './components/PaginatePost.vue';
import BlogPost from './components/BlogPost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';
import { ref, computed, onMounted } from 'vue';

const posts = ref([]);
const postForPage = 10;
const start = ref(0);
const end = ref(postForPage);
const loading = ref(true);

const favorito = ref('');

const favChange = (title) => {
  favorito.value = title;
};

const next = () => {
  start.value += postForPage;
  end.value += postForPage;
}

const prev = () => {
  start.value -= postForPage;
  end.value -= postForPage;
}

const maxLength = computed(() => posts.value.length)

/* onMounted(async() => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(() => {
      loading.value = false;
    }, 2000)
  }
}); */

/* fetch('https://jsonplaceholder.typicode.com/posts')
  .then(res => res.json())
  .then(data => posts.value = data)
  .catch(error => console.log(error))
  .finally(() => {
    setTimeout(() => {
      loading.value = false
    }, 2000)
}); */

const fetchData = async() => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(() => {
      loading.value = false;
    }, 2000)
  }
};

fetchData();
</script>

<template>
  <LoadingSpinner v-if="loading"/>
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mi post favorito: {{ favorito }}</h2>

    <PaginatePost 
      @prevPage="prev" 
      @nextPage="next" 
      :start="start" 
      :end="end"
      :maxLength="maxLength" 
      class="mb-2"
    />

    <BlogPost v-for="post in posts.slice(start, end)"
    :key="post.id"
    :id="post.id" 
    :title="post.title" 
    :body="post.body"
    @favPost="favChange"
    class="mb-2"
    ></BlogPost>
  </div>
</template>