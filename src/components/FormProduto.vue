<!-- ProdutoForm.vue -->

<template>
    <div>
        <div v-if="showSuccessAlert" class="alert alert-success" role="alert">
            Produto salvo com sucesso!
          </div>

          <form @submit.prevent="submitForm">
            <div class="mb-3">
              <label for="nome" class="form-label">Nome do Produto</label>
              <input v-model="produto.nome" type="text" class="form-control" id="nome" required>
            </div>
        
            <div class="mb-3">
              <label for="descricao" class="form-label">Descrição do Produto</label>
              <textarea v-model="produto.descricao" class="form-control" id="descricao" rows="3" required></textarea>
            </div>
        
            <div class="mb-3">
              <label for="preco" class="form-label">Preço por Unidade</label>
              <input v-model="produto.precoPorUnidade" type="number" step="0.01" class="form-control" id="preco" required>
            </div>
        
            <div class="mb-3">
              <label for="quantidade" class="form-label">Quantidade em Estoque</label>
              <input v-model="produto.quantidadeEmEstoque" type="number" class="form-control" id="quantidade" required>
            </div>
        
            <div class="mb-3">
              <label for="categoria" class="form-label">Categoria</label>
              <select v-model="produto.idCategoria" class="form-select" id="categoria" required>
                <option v-for="categoria in categorias" :key="categoria.id" :value="categoria.id">{{ categoria.nome }}</option>
              </select>
            </div>
        
            <button type="submit" class="btn btn-primary">Salvar Produto</button>
          </form>
    </div>
   
  </template>
  
  <script>
   import axios from 'axios';
  export default {
    data() {
      return {
        produto: {
          nome: '',
          descricao: '',
          precoPorUnidade: 0,
          quantidadeEmEstoque: 0,
          idCategoria: null
        },
        categorias: [],
        showSuccessAlert: false
      };
    },
    mounted() {
      // Busca as categorias da API
      // Certifique-se de instalar o axios com npm install axios
  
      axios.get('http://191.101.234.241:3000/categoria')
        .then(response => {
          this.categorias = response.data;
        })
        .catch(error => {
          console.error('Erro ao carregar categorias:', error);
        });
    },
    methods: {
        submitForm() {
      // Certifique-se de instalar o axios com npm install axios
      
      axios.post('http://191.101.234.241:3000/produto', this.produto)
        .then(response => {
          console.log('Produto salvo com sucesso:', response.data);
          this.showSuccessAlert = true;  // Ativa o alerta de sucesso
          this.produto=[]
          // Pode ser desativado após alguns segundos, se desejado
          setTimeout(() => {
            this.showSuccessAlert = false;
          }, 5000);
        })
        .catch(error => {
          console.error('Erro ao salvar produto:', error);
        });
    }
    }
  };
  </script>
  