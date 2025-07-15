<script setup>
// Os dados dos benefícios serão um array de objetos,
// o que facilita a manutenção e renderização com v-for.
const benefits = [
  {
    id: 1,
    subtitle: 'ECONOMIA COM O VALOR DE CUSTO DO PRODUTO',
    title: 'Reduza custos antes do lançamento!',
    description: 'Identifique e corrija erros antes de colocar seu produto no mercado e evite gastos desnecessários com retrabalho. Empresas que investem em testes de qualidade economizam até ',
    highlight: '30%',
    highlightText: 'no custo total do desenvolvimento.',
    image: '../assets/images/custos.jpg'
  },
  {
    id: 2,
    subtitle: 'MELHORIA DE TEMPO E PERFORMANCE DO PRODUTO',
    title: 'Mais rápido, mais eficiente!',
    description: 'Testes de qualidade garantem um software otimizado, reduzindo tempo de resposta e aumentando a performance. Empresas que priorizam QA têm ',
    highlight: '40%',
    highlightText: 'menos falhas críticas e entregam produtos mais ágeis ao mercado',
    image: '../assets/images/melhorias.jpg'
  },

  {
    id: 3,
    ubtitle: 'MAIOR ADESÃO DO USUÁRIO FINAL',
    title: 'Usuários felizes, marca fortalecida!',
    description: 'A satisfação do cliente começa com um produto livre de falhas. Corrigir bugs antes do lançamento aumenta a adesão e a confiança do usuário, reduzindo reclamações e melhorando avaliações em até',
    highlight: '45%',
    highlightText: ', tornando sua marca líder em qualidade.',
    image: '../assets/images/usuariofeliz.jpg'
  }
];
</script>

<template>
  <section id="benefits" class="benefits-section">
    <div class="container">
      <h2>Benefícios de Investir em Qualidade de Software</h2>
      <div class="benefits-grid">
        <article v-for="benefit in benefits" :key="benefit.id" class="benefit-card">
          <div class="card-content">
            <p class="card-subtitle">{{ benefit.subtitle }}</p>
            <h3>{{ benefit.title }}</h3>
            <p class="card-description">{{ benefit.description }} <span class="highlight">{{ benefit.highlight }}</span> <strong class="highlightText">{{ benefit.highlightText }}</strong></p>
          </div>
          <div v-if="benefit.image" class="card-image">
            <img :src="`src/assets/${benefit.image}`" :alt="benefit.title" />
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.benefits-section {
  padding: var(--spacing-lg) var(--spacing-md); /* Usando variáveis para padding */
  background: linear-gradient(231deg,rgba(144, 0, 255, 0.637) 0%, rgba(102, 52, 138, 0.671) 50%, rgba(211, 167, 242, 0.884) 100%);
  color: var(--color-dark); /* Usando variável para cor do texto */
}

/* O .container aqui pode ser removido, já que você tem um .container global em main.css
   que já faz a centralização e padding. Se você tiver um div com classe `container`
   dentro do template desta seção, ele já pegará os estilos globais. */
/* .container {
   max-width: var(--max-width-desktop, 1120px);
   margin: 0 auto;
} */

.benefits-section h2 {
  text-align: center;
  font-size: var(--font-size-xl); /* Usando variável para o título da seção */
  margin-bottom: var(--spacing-lg); /* Usando variável para espaçamento */
  color: var(--color-white); /* Usando variável */
  text-shadow: 1px 2px 5px var(--color-dark);
}

.benefits-grid {
  display: flex;
  flex-direction: column; /* Em coluna por padrão para mobile */
  gap: var(--spacing-md); /* Usando variável para espaçamento entre os cards */
}

.benefit-card {
  background-color: var(--color-white); /* Usando variável */
  padding: var(--spacing-md); /* Usando variável para padding interno do card */
  border-radius: 12px;
  box-shadow: 0 5px 25px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column; /* Conteúdo interno do card em coluna */
  align-items: center;
  text-align: center;
}
.benefit-card:hover {
  transform: translateY(-2px); /* Efeito de levantar o card */
  box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.479); /* Sombra suave */
}
/* Alternar o layout dos cards em telas maiores */
.benefits-grid .benefit-card:nth-child(even) {
  flex-direction: row-reverse; /* Imagem à esquerda, texto à direita */
}
.benefits-grid .benefit-card:nth-child(odd) {
  flex-direction: row; /* Imagem à direita, texto à esquerda */
}

@media (max-width: 767px) {
  .benefit-card,
  .benefits-grid .benefit-card:nth-child(even),
  .benefits-grid .benefit-card:nth-child(odd) {
    flex-direction: column; /* Força coluna em mobile */
    text-align: justify;
  }
  .card-image {
    display: none;
    order: -1; /* Coloca a imagem acima do texto em mobile */
    margin-bottom: var(--spacing-sm); /* Usando variável */
  }
  .card-content {
    padding-right: 0;
    padding-left: 0;
  }
  /* Ajustes de fonte para mobile, se necessário */
  .benefits-section h2 {
      font-size: var(--font-size-xl);
      margin-bottom: var(--spacing-md);
  }
  .benefit-card h3 {
      font-size: var(--font-size-lg);
  }
  .card-description {
      font-size: var(--font-size-base);
  }
  .highlight {
      font-size: var(--font-size-xl); /* Ajustar tamanho em mobile */
  }
  .highlightText {
      font-size: var(--font-size-base); /* Ajustar tamanho em mobile */
  }
}


.card-content {
  flex: 2;
  padding-right: var(--spacing-md); /* Usando variável */
}
.benefits-grid .benefit-card:nth-child(even) .card-content {
  padding-left: var(--spacing-md); /* Inverte o padding para cards pares */
  padding-right: 0;
}


.card-image {
  flex: 1;
  min-width: 200px;
  max-width: 300px;
}

.card-image img {
  width: 100%;
  height: auto;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.card-subtitle {
  font-size: var(--font-size-sm); /* Usando variável */
  color: var(--color-secondary); /* Usando variável para cinza */
  margin-bottom: var(--spacing-xs); /* Usando variável */
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.benefit-card h3 {
  font-size: var(--font-size-xl); /* Usando variável para o título do benefício */
  font-weight: bold;
  margin-bottom: var(--spacing-sm); /* Usando variável */
  color: var(--color-dark); /* Usando variável */
}

.card-description {
  font-size: var(--font-size-md); /* Usando variável */
  line-height: 1.6;
  margin-bottom: var(--spacing-sm); /* Usando variável */
  color: var(--color-dark); /* Garante a cor consistente */
}

.highlight {
  font-size: var(--font-size-xxl); /* Usando variável para o percentual */
  font-weight: bold;
  color: var(--color-accent); /* Usando variável para cor roxa */
  display: inline-block;
  line-height: 1;
  vertical-align: baseline;
  margin-right: var(--spacing-xs);
  margin-left: var(--spacing-xs);
}

.highlightText {
  font-size: var(--font-size-lg); /* Usando variável */
  color: var(--color-dark); /* Garante a cor consistente */
  font-weight: bold; /* Já é strong, mas garante se mudar a tag */
}
</style>
