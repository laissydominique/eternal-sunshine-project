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

const cont = ref(1);

setInterval(() => {
  proximaImg();
}, 5000);

function proximaImg() {
  cont.value++;
  if (cont.value > 3) {
    cont.value = 1;
  }
}

onMounted(() => {
  getJoias();
  proximaImg();
});
</script>

<template>
  <div class="container">
    <header>
      <div class="cabecalho">
        <div class="rotas">
          <p class="home">Store ✦ Home ✦ About Us</p>
        </div>
        <div class="icon">
          <img src="./img/icon2.png" alt="" width="120px" />
        </div>
      </div>
    </header>
    <div class="saudacao">
      <h1>Eternal Sunshine Jewelry</h1>
      <h2>Make it shine</h2>
    </div>

    <section class="slider">
      <div class="slider-content">
        <input
          type="radio"
          name="btn-radio"
          id="radio1"
          value="1"
          v-model="cont"
        />
        <input
          type="radio"
          name="btn-radio"
          id="radio2"
          value="2"
          v-model="cont"
        />
        <input
          type="radio"
          name="btn-radio"
          id="radio3"
          value="3"
          v-model="cont"
        />

        <div class="slider-box primeiro">
          <img
            class="img-desktop"
            src="./img/banner.png"
            alt=""
            width="1700px"
            height="750px"
          />
          <img
            class="img-mobile"
            src="./img/banner.png"
            alt=""
            width="700px"
            height="500px"
          />
        </div>
        <div class="slider-box">
          <img
            class="img-desktop"
            src="./img/image5.png"
            alt=""
            width="1700px"
            height="750px"
          />

          <img
            class="img-mobile"
            src="./img/image5.png"
            alt=""
            width="700px"
            height="500px"
          />
        </div>
        <div class="slider-box">
          <img
            class="img-desktop"
            src="./img/banner_tres.jpg"
            alt=""
            width="1700px"
            height="750px"
          />

          <img
            class="img-mobile"
            src="./img/banner_tres.jpg"
            alt=""
            width="700px"
            height="500px"
          />
        </div>

        <div class="nav-auto">
          <div class="auto-btn1"></div>
          <div class="auto-btn2"></div>
          <div class="auto-btn3"></div>
        </div>

        <div class="nav-manual">
          <label for="radio1" class="manual-btn"></label>
          <label for="radio2" class="manual-btn"></label>
          <label for="radio3" class="manual-btn"></label>
        </div>
      </div>
    </section>

    <div class="subtitulo">
      <h3>Our products</h3>
    </div>

    <div class="joias">
      <div class="joia" v-for="joia in info.itens" :key="joia.titulo">
        <p class="titulo">{{ joia.titulo }}</p>
        <div class="imagem">
          <img
            :src="joia.imagem"
            alt="Imagem da jóia"
            style="width: 300px; height: 250px"
          />
        </div>

        <p class="valor">$ {{ joia.preco }}</p>
        <div class="divbuy">
          <p class="comprar">Buy now</p>
        </div>
        <p class="descricao">{{ joia.descricao }}</p>
        <p class="avaliacao">{{ joia.rating }} ({{ joia.count }} reviews)</p>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
