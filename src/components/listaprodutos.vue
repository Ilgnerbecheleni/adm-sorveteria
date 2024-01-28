<!-- ProdutoCardList.vue -->

<template>
    <div>
      <div v-for="produto in produtos" :key="produto.id" class="card" style="width: 18rem; margin: 10px;">
        <img :src="getImagemUrl(produto.id)" class="card-img-top" alt="Imagem do Produto">
        <div class="card-body">
          <h5 class="card-title">{{ produto.nome }}</h5>
          <p class="card-text">{{ produto.descricao }}</p>
          <a :href="getImagemUrl(produto.id)" class="btn btn-primary" target="_blank">Ver Imagem</a>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        produtos: [],
        imagens: []
      };
    },
    mounted() {
      this.carregarProdutos();
      this.carregarImagens();
    },
    methods: {
      carregarProdutos() {
        axios.get('http://191.101.234.241:3000/produto')
          .then(response => {
            this.produtos = response.data;
          })
          .catch(error => {
            console.error('Erro ao carregar produtos:', error);
          });
      },
      carregarImagens() {
        axios.get('http://191.101.234.241:3000/files')
          .then(response => {
            this.imagens = response.data;
          })
          .catch(error => {
            console.error('Erro ao carregar imagens:', error);
          });
      },
      getImagemUrl(idProduto) {
        const imagem = this.imagens.find(img => img.idProduto === idProduto);
        return imagem ? imagem.url : 'placeholder_url'; // Substitua 'placeholder_url' pela URL de uma imagem padrão, se necessário
      }
    }
  };
  </script>
  
  <style>
  /* Adicione estilos conforme necessário */
  </style>
  