<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else>
    <h1>
      APP
    </h1>
    <h2>Mis post favorito: {{ favorito || "Sin favorito" }}</h2>
    <PaginatePost class="mb-2" @next="next" @previous="previous" :inicio="inicio" :fin="fin" :postsLength="postsLength"/>
    <BlogPost class="mb-2" v-for="post in posts.slice(inicio,fin)" :key="post.id" :title="post.title" :id="post.id" :body="post.body" :colorText="post.colorText" @cambiarFavoritoNombre="cambiarFavorito"/>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

const posts = ref([]);
const postXPage = 10;
const inicio = ref(0);
const fin = ref(postXPage);
const loading = ref(true);

const favorito = ref('')
const cambiarFavorito = title => {
  favorito.value = title
}
const next = () => {
  inicio.value += + postXPage;
  fin.value += + postXPage;
}
const previous = () => {
  inicio.value += - postXPage;
  fin.value += - postXPage;
}

onMounted(async() => {
  try{
     const res = await fetch('https://jsonplaceholder.typicode.com/posts');
     posts.value = await res.json();
  } catch(e){
    console.log(e);
  }finally{
    loading.value = false;
  }
})

// fetch('https://jsonplaceholder.typicode.com/posts')
//   .then(response => response.json())
//   .then(data => posts.value = data)
//   .catch(e => console.log(e))
//   .finally(() => loading.value = false)

const postsLength = computed(() => posts.value.length)
</script>
