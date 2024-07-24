<script setup>
import { ref, onMounted } from "vue";

const info = ref({
  itens: [],
});

async function getJoias() {
  const response = await fetch(
    `https://fakestoreapi.com/products/category/jewelery`
  );
  const data = await response.json();
  console.log(data);

  info.value.itens = data.map((item) => ({
    titulo: item.title,
    imagem: item.image,
    preco: item.price,
    descricao: item.description,
    rating: item.rating.rate,
    count: item.rating.count,
  }));
}

onMounted(() => {
  getJoias();
});
</script>

<template>
  <div class="container">
    <div class="saudacao" >
      <h1>Eternal Sunshine Jewelry</h1>
      <h2>Make it shine</h2>
    </div>
    <div class="joias"> 
    <div class="joia" v-for="joia in info.itens" :key="joia.titulo">
      <p>{{ joia.titulo }}</p>
      <div class="imagem">
        <img
          :src="joia.imagem"
          alt="Imagem da jóia"
          style="width: 115px; height: 110px"
        />
      </div>
      <p>$ {{ joia.preco }}</p>
      <p>{{ joia.descricao }}</p>
      <p>{{ joia.rating }} ({{ joia.count }} reviews)</p>
    </div>
  </div>
  </div>
</template>

<style scoped></style>
