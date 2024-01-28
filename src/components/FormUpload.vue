<!-- ProdutoFotoForm.vue -->

<template>
    <div>
      <!-- Adiciona o alerta de sucesso -->
      <div v-if="showSuccessAlert" class="alert alert-success" role="alert">
        Foto adicionada com sucesso para o Produto {{ produtoSelecionado }}
      </div>
  
      <form @submit.prevent="submitForm">
        <div class="mb-3">
          <label for="produto" class="form-label">Escolha um Produto</label>
          <select v-model="produtoSelecionado" class="form-select" required>
            <option v-for="produto in produtos" :key="produto.id" :value="produto.id">{{ produto.nome }}</option>
          </select>
        </div>
  
        <div class="mb-3">
          <label for="foto" class="form-label">Selecione uma Foto</label>
          <input type="file" @change="handleFileChange" class="form-control" name="arquivo" required>
        </div>
  
        <button type="submit" class="btn btn-primary">Adicionar Foto</button>
      </form>
    </div>
  </template>
  
  <script>
  // Importa as bibliotecas necessárias no início do script
  import axios from 'axios';
  
  export default {
    data() {
      return {
        produtoSelecionado: null,
        produtos: [],  // Lista de produtos a serem carregados
        foto: null,  // Arquivo da foto a ser enviado
        showSuccessAlert: false  // Adiciona uma propriedade para controlar a exibição do alerta
      };
    },
    mounted() {
      // Carrega a lista de produtos da API
      axios.get('http://191.101.234.241:3000/produto')
        .then(response => {
          this.produtos = response.data;
        })
        .catch(error => {
          console.error('Erro ao carregar produtos:', error);
        });
    },
    methods: {
      handleFileChange(event) {
        // Atualiza a variável 'foto' quando o arquivo é alterado
        this.foto = event.target.files[0];
      },
      submitForm() {
        // Cria um objeto FormData para enviar a foto
        let formData = new FormData();
        formData.append('arquivo', this.foto);  // O nome do campo é ajustado para 'arquivo'
  
        // Realiza a requisição para adicionar a foto ao produto selecionado
        axios.post(`http://191.101.234.241:3000/files/${this.produtoSelecionado}`, formData)
          .then(response => {
            console.log('Foto adicionada com sucesso:', response.data);
            this.showSuccessAlert = true;  // Ativa o alerta de sucesso
            
            // Pode ser desativado após alguns segundos, se desejado
            setTimeout(() => {
              this.showSuccessAlert = false;
            }, 5000);
          })
          .catch(error => {
            console.error('Erro ao adicionar foto:', error);
          });
      }
    }
  };
  </script>
  