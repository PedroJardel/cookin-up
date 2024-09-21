<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { obterReceitas } from '@/http';
import type IReceita from '@/interfaces/IReceita';
import BotaoPrincipal from './BotaoPrincipal.vue';
import CardReceita from './CardReceita.vue';

const receitas = ref<IReceita[]>([])

const buscarReceitas = async () => {
    try {
        receitas.value = await obterReceitas()
    } catch (error) {
        console.error('Erro ao buscar receitas:', error);
    }
}

const emits = defineEmits(['VoltarSelecao'])

onMounted(() => {
    buscarReceitas();
});
</script>

<template>
    <section class="selecionar-ingredientes">
        <h1 class="cabecalho titulo-ingredientes">Receitas</h1>
        <p class="paragrafo-lg resultado">
            Resultados encontrados: {{ receitas.length }}
        </p>
        <div v-if="receitas.length" class="conteudo-principal">
            <p class="paragrafo-lg instrucoes">
                Veja as opções de receitas que encontramos com os ingredientes que você tem por aí!
            </p>
            <ul class="receitas">
                <li v-for="receita in receitas" :key="receita.nome">
                    <CardReceita :receita="receita" />
                </li>
            </ul>
        </div>
        <div v-else class="conteudo-principal">
            <p class="paragrafo-lg instrucoes">
                Ops, não encontramos resultador para a sua combinação. Vamos tentar de novo?
            </p>
            <img src="../assets/images/sem-receitas.png" alt="" class="lista-vazia">
        </div>
        <BotaoPrincipal :texto="'Editar Lista'" @click="$emit('VoltarSelecao')" />
    </section>
</template>

<style scoped>
.conteudo-principal {
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
.selecionar-ingredientes {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.titulo-ingredientes {
    color: var(--verde-medio, #3D6D4A);
    display: block;
    margin-bottom: 1.5rem;
}
.resultado {
    color: var(--verde-medio)
}

.instrucoes {
    margin-bottom: 2rem;
}

.receitas {
    margin-bottom: 1rem;
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    flex-wrap: wrap;
}
</style>