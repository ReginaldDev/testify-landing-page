<script setup>
import { onMounted, ref } from 'vue'

import UsuarioFeliz from '@/assets/images/usuariofeliz.jpg'
import CustosImg from '@/assets/images/custos.jpg'
import MelhoriasImg from '@/assets/images/melhorias.jpg'

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
    image: CustosImg,
    visible: ref(false),
    direction: 'left' // Animação virá da esquerda
  },
  {
    id: 2,
    subtitle: 'MELHORIA DE TEMPO E PERFORMANCE DO PRODUTO',
    title: 'Mais rápido, mais eficiente!',
    description: 'Testes de qualidade garantem um software otimizado, reduzindo tempo de resposta e aumentando a performance. Empresas que priorizam QA têm ',
    highlight: '40%',
    highlightText: 'menos falhas críticas e entregam produtos mais ágeis ao mercado',
    image: MelhoriasImg,
    visible: ref(false),
    direction: 'right' // Animação virá da direita
  },
  {
    id: 3,
    subtitle: 'MAIOR ADESÃO DO USUÁRIO FINAL',
    title: 'Usuários felizes, marca fortalecida!',
    description: 'A satisfação do cliente começa com um produto livre de falhas. Corrigir bugs antes do lançamento aumenta a adesão e a confiança do usuário, reduzindo reclamações e melhorando avaliações em até',
    highlight: '45%',
    highlightText: ', tornando sua marca líder em qualidade.',
    image: UsuarioFeliz,
    visible: ref(false),
    direction: 'left' // Animação virá da esquerda
  }
];

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      const benefit = benefits.find(b => b.id.toString() === entry.target.dataset.benefitId);
      if (benefit) {
        if (entry.isIntersecting) {
          benefit.visible.value = true;
        } else {
          // Remove a visibilidade para a animação ser reativada ao rolar de volta
          benefit.visible.value = false;
        }
      }
    });
  }, {
    threshold: 0.2
  });

  document.querySelectorAll('.benefit-card').forEach(card => {
    observer.observe(card);
  });
});
</script>

<template>
  <section id="benefits" class="benefits-section">
    <div class="container">
      <h2>Benefícios de Investir em Qualidade de Software</h2>
      <div class="benefits-grid">
        <article
          v-for="benefit in benefits"
          :key="benefit.id"
          :class="['benefit-card', { 'is-visible': benefit.visible.value, 'from-left': benefit.direction === 'left', 'from-right': benefit.direction === 'right' }]"
          :data-benefit-id="benefit.id"
        >
          <div class="card-content">
            <p class="card-subtitle">{{ benefit.subtitle }}</p>
            <h3>{{ benefit.title }}</h3>
            <p class="card-description">{{ benefit.description }} <span class="highlight">{{ benefit.highlight }}</span> <strong class="highlightText">{{ benefit.highlightText }}</strong></p>
          </div>
          <div v-if="benefit.image" class="card-image">
            <img :src="benefit.image" :alt="benefit.title" />
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.benefits-section {
  padding: var(--spacing-lg) var(--spacing-md);
  background: linear-gradient(231deg,rgba(144, 0, 255, 0.637) 0%, rgba(102, 52, 138, 0.671) 50%, rgba(211, 167, 242, 0.884) 100%);
  color: var(--color-dark);
}

.benefits-section h2 {
  text-align: center;
  font-size: var(--font-size-xl);
  margin-bottom: var(--spacing-lg);
  color: var(--color-white);
  text-shadow: 1px 2px 5px var(--color-dark);
}

.benefits-grid {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

.benefit-card {
  background-color: var(--color-white);
  padding: var(--spacing-md);
  border-radius: 12px;
  box-shadow: 0 5px 25px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  opacity: 0;
  transition: opacity 0.6s ease-out, transform 0.6s ease-out;
}

.benefit-card:hover {
  transform: translateY(-2px);
  box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.479);
}

/* 1. Animações de entrada */
/* Animação para cards que vêm da esquerda */
.benefit-card.from-left {
  transform: translateX(-50px);
}
/* Animação para cards que vêm da direita */
.benefit-card.from-right {
  transform: translateX(50px);
}

/* 2. Estado visível */
.benefit-card.is-visible {
  opacity: 1;
  transform: translateX(0);
}

/* 3. Atraso na animação */
.benefits-grid .benefit-card:nth-child(2) {
  transition-delay: 0.2s;
}
.benefits-grid .benefit-card:nth-child(3) {
  transition-delay: 0.3,5s;
}

/* Estilos de layout alternado para desktop */
@media (min-width: 768px) {
  .benefits-grid .benefit-card:nth-child(even) {
    flex-direction: row-reverse;
  }
  .benefits-grid .benefit-card:nth-child(odd) {
    flex-direction: row;
  }
}

/* Ajustes para mobile */
@media (max-width: 767px) {
  .benefit-card,
  .benefits-grid .benefit-card:nth-child(even),
  .benefits-grid .benefit-card:nth-child(odd) {
    flex-direction: column;
    text-align: justify;
  }
  .card-image {
    display: none;
  }
  .card-content {
    padding-right: 0;
    padding-left: 0;
  }
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
      font-size: var(--font-size-xl);
  }
  .highlightText {
      font-size: var(--font-size-base);
  }
}

.card-content {
  flex: 2;
  padding-right: var(--spacing-md);
}
.benefits-grid .benefit-card:nth-child(even) .card-content {
  padding-left: var(--spacing-md);
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
  font-size: var(--font-size-sm);
  color: var(--color-secondary);
  margin-bottom: var(--spacing-xs);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.benefit-card h3 {
  font-size: var(--font-size-xl);
  font-weight: bold;
  margin-bottom: var(--spacing-sm);
  color: var(--color-dark);
}

.card-description {
  font-size: var(--font-size-md);
  line-height: 1.6;
  margin-bottom: var(--spacing-sm);
  color: var(--color-dark);
}

.highlight {
  font-size: var(--font-size-xxl);
  font-weight: bold;
  color: var(--color-accent);
  display: inline-block;
  line-height: 1;
  vertical-align: baseline;
  margin-right: var(--spacing-xs);
  margin-left: var(--spacing-xs);
}

.highlightText {
  font-size: var(--font-size-lg);
  color: var(--color-dark);
  font-weight: bold;
}
</style>
