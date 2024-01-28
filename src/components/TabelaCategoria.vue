<template>
    <div class="container mt-5">
      <h2>Lista de Categorias</h2>
      <table class="table">
        <thead>
          <tr>
            <th>ID</th>
            <th>Nome</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="categoria in categorias" :key="categoria.id">
            <td>{{ categoria.id }}</td>
            <td>{{ categoria.nome }}</td>
            <td><button class="btn danger">Excluir</button></td>
            <td><button class="btn btn-danger" @click="excluirCategoria(categoria.id)">Excluir</button></td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      categorias: {
        type: Array,
        required: true,
      },
      excluirCategoria: {
      type: Function,
      required: true,
    },
    
    },
  };
  </script>
  
  <style scoped>
  /* Adicione estilos conforme necessário */
  </style>
  