<script setup>
import { ref } from 'vue';
import ProdutoChild from './components/ProdutoChild.vue';
import { listaProdutos } from './data/Produtos';
import { formataPreco } from './utils/produtoUtils';
const produtos = ref(listaProdutos);

const preco = ref(0);

const posicaoProduto = ref (-1)
const alterando = ref(false);

function corrigirPreco(idProduto, precoProduto) {
  preco.value = precoProduto
  posicaoProduto.value = produtos.value.findIndex(p => p.id === idProduto)
  alterando.value = true;
}

function salvarPreco(){
  produtos.value[posicaoProduto.value].preco = preco.value
  alterando.value = false;
}

</script>

<template>
  <div class="container">
    <h1>Catálogo de Produtos</h1>
    <div>
      <ul>
        <ProdutoChild v-for="produto in produtos" 
        :key="produto.id" 
        :id="produto.id" 
        :nome="produto.nome"
        :preco="produto.preco" 
        :categoria="produto.categoria" 
        @corrigirpreco = "corrigirPreco">
          <button @click.prevent="corrigirPreco(produto.id, produto.preco)">Corrigir Preço</button>
        </ProdutoChild>
      </ul>
    </div>
    <div v-show="alterando">
      <label>Preço</label>
      <input type="number" v-model="preco" placeholder="Ex:R$200">
      <button @click.prevent="salvarPreco()">Salvar</button>
    </div>
  </div>
</template>

<style scoped></style>
