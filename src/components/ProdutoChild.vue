<script setup>
defineProps(['nome', 'preco', 'categoria', 'id'])
defineEmits(['corrigirpreco'])
import { formataPreco } from '@/utils/produtoUtils';
import ButtonChild from './ButtonChild.vue';
</script>

<template>
<li>
    {{ nome }} -  {{ formataPreco(preco) }} ({{ categoria }})
    <ButtonChild @clique="$emit('corrigirpreco',id ,preco)">
        Corrigir preço
    </ButtonChild>
</li>
</template>

<style scoped>

</style>