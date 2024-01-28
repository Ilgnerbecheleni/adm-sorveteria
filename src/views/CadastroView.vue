<script>
import FormCategoria from '@/components/FormCategoria.vue';
import FormProduto from '@/components/FormProduto.vue';
import FormUpload from '@/components/FormUpload.vue';
import TabelaCategoria from '@/components/TabelaCategoria.vue';
export default {
  components: {
    FormCategoria,
    TabelaCategoria,
    FormProduto,
    FormUpload
},
data() {
    return {
      categorias: [],
    };
  },
  methods: {
    async fetchCategorias() {
      try {
        this.categoria=[]
        const response = await fetch('http://191.101.234.241:3000/categoria');
        if (response.ok) {
          const data = await response.json();
          this.categorias = data;
        } else {
          console.error('Erro ao obter categorias:', response.statusText);
        }
      } catch (error) {
        console.error('Erro ao obter categorias:', error);
      }
    },
    async handleMensagem({ sucesso }) {
      if (sucesso) {
        console.log('sucesso')
        // Se o cadastro foi bem-sucedido, recarregue a lista de categorias
        await this.fetchCategorias();
      }
    },
    async excluirCategoria(id) {
      try {
        if(confirm('Quer deletar a categoria com id '+ id))
       { 
        const response = await fetch(`http://191.101.234.241:3000/categoria/${id}`, {
          method: 'DELETE',
        });

        if (response.ok) {
          // Excluir a categoria localmente
          this.categorias = this.categorias.filter(categoria => categoria.id !== id);
          console.log(`Categoria com ID ${id} excluída com sucesso.`);
        } else {
          console.error(`Erro ao excluir categoria com ID ${id}:`, response.statusText);
        }
      }
      } catch (error) {
        console.error(`Erro ao excluir categoria com ID ${id}:`, error);
      }
    },
  },
  mounted() {
    this.fetchCategorias();
  },
};

</script>
<template>
<main>
  <FormCategoria  @mensagem="handleMensagem" />
  <TabelaCategoria :categorias="categorias" :excluirCategoria="excluirCategoria" />
  <FormProduto @mensagem="handleMensagem" />
  <FormUpload />
</main>
</template>

<style>

</style>
