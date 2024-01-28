<template>
    <div class="container mt-5">
      <h2>Cadastrar Nova Categoria</h2>
      <form @submit.prevent="submitCategoria">
        <div class="mb-3">
          <label for="nome" class="form-label">Nome da Categoria:</label>
          <input v-model="nome" type="text" class="form-control" id="nome" required />
        </div>
  
        <button type="submit" class="btn btn-primary">Cadastrar Categoria</button>
      </form>
  
      <p v-if="mensagem" class="alert" :class="{ 'alert-success': sucesso, 'alert-danger': !sucesso }">{{ mensagem }}</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        nome: '',
        mensagem: '',
        sucesso: false,
      };
    },
    methods: {
      async submitCategoria() {
        try {
          const response = await fetch('http://191.101.234.241:3000/categoria', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json',
            },
            body: JSON.stringify({ nome: this.nome }),
          });
  
          if (response.ok) {
            // Exemplo de sucesso
            this.mensagem = 'Categoria cadastrada com sucesso!';
            this.sucesso = true;
  
            // Limpar o campo após o sucesso, se desejado
            this.nome = '';
  
            // Remover a mensagem após 3 segundos (3000 milissegundos)
            setTimeout(() => {
              this.mensagem = '';
            }, 3000);
          } else {
            // Exemplo de falha
            this.mensagem = 'Erro ao cadastrar categoria. Por favor, tente novamente.';
            this.sucesso = false;
          }
        } catch (error) {
          console.error('Erro ao cadastrar categoria:', error);
  
          // Exemplo de falha
          this.mensagem = 'Erro ao cadastrar categoria. Por favor, tente novamente.';
          this.sucesso = false;
        }
      },
    },
  };
  </script>
  
  <style scoped>
  /* Estilos personalizados, se necessário */
  </style>
  