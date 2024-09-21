<script setup lang="ts">
import type { PropType } from 'vue';
import type IReceita from '@/interfaces/IReceita';

const props = defineProps<{
    receita: IReceita
}>()

</script>

<template>
    <article class="receita">
        <header class="receita__cabecalho">
            <img :src="`/imagens/receitas/${receita.imagem}`" alt="" class="receita__imagem">
            <h2 class="paragrafo-lg receita__nome">
                {{ receita.nome }}
            </h2>
        </header>
    </article>
</template>

<style scoped>
.receita {
    width: 19.5rem;
    border-radius: 1rem;
    background: var(--branco, #FFF);
    box-shadow: 4px 4px 10px 0px rgba(68, 68, 68, 0.05);
    height: 100%;

    display: flex;
    flex-direction: column;
    gap: 2rem;
    overflow: hidden;
}

.receita__cabecalho {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
}

.receita__imagem {
    width: 100%;
    height: auto;
}

.receita__nome {
    text-align: center;
    color: var(--cinza, #444444);
    font-weight: 700;
    padding: 1.5rem 0rem;
}

.receita__ingredientes {
    display: flex;
    justify-content: center;
    gap: 0.5rem;
    flex-wrap: wrap;
}
</style>