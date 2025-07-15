<script setup>
import { ref, computed } from 'vue';

// 1. IMPORTAR AS IMAGENS: Esta é a maneira correta para caminhos dentro de 'src/assets'
import historyImage from '../assets/images/about/about1.jpg';
import whatWeDoImage from '../assets/images/about/about2.jpg';
import whyChooseImage from '../assets/images/about/about3.jpg';

// 2. Dados dos blocos de informação - Usando as variáveis importadas
const infoBlocks = ref([
  {
    id: 'historia',
    title: 'Nossa História',
    image: historyImage, // Usando a variável importada
    content: [
      `A Testfy nasceu da amizade entre profissionais que trilharam juntos a jornada da tecnologia, enfrentando os desafios do dia a dia como QAs e desenvolvedores. Entre cafés, códigos e bugs resolvidos, surgiu uma ideia em comum: criar algo com propósito real.`,
      `Depois de anos atuando em projetos de diversos portes e setores, percebemos uma lacuna no mercado — a qualidade de software muitas vezes era deixada de lado até que os problemas se tornassem críticos. Decidimos mudar esse cenário. Unimos nossas experiências, talentos e visão para fundar uma startup focada em prevenir falhas antes que elas aconteçam.`,
      `Hoje, a Testfy é fruto dessa união: um time que compartilha valores, trabalha com confiança mútua e acredita que qualidade é construída desde o início.`
    ]
  },
  {
    id: 'o-que-fazemos',
    title: 'O Que Fazemos',
    image: whatWeDoImage, // Usando a variável importada
    content: [
      `Na Testfy, oferecemos serviços especializados em testes de software para aplicações Web, Backend e APIs. Atuamos com foco em garantir que seu sistema funcione de forma eficiente, segura e com a melhor experiência para o usuário.`,
      `Executamos testes funcionais, de performance, segurança, usabilidade, automação e testes exploratórios sob demanda, com metodologias adaptadas à necessidade de cada projeto. Nossa abordagem é colaborativa: entendemos o seu negócio, identificamos riscos e entregamos relatórios claros, com recomendações práticas.`,
      `Trabalhamos com as ferramentas mais modernas do mercado, mas nosso maior diferencial está no olhar atento de quem entende o impacto de cada detalhe em produção.`
    ]
  },
  {
    id: 'por-que-escolher',
    title: 'Por Que Escolher a Testfy',
    image: whyChooseImage, // Usando a variável importada
    content: [
      `Porque somos movidos por propósito. Nossa equipe carrega não apenas conhecimento técnico, mas uma trajetória real dentro do universo do desenvolvimento de software. Já estivemos do outro lado — enfrentando bugs em produção, lidando com prazos apertados e clientes exigentes. Sabemos o quanto a qualidade importa.`,
      `Acreditamos que testes bem feitos são a base para qualquer sistema de sucesso. E qualidade não se improvisa: se constrói com experiência, comprometimento e parceria.`,
      `Se você busca uma equipe que se envolve de verdade, se comunica com clareza e entrega resultados sólidos, a Testfy é a escolha certa.`,
      `Aqui, qualidade é compromisso.`
    ]
  }
]);

// 3. Estado reativo para controlar a aba ativa
const activeTabId = ref(infoBlocks.value[0].id); // Começa com "Nossa História"

// 4. Computed property para obter o bloco de informação ativo
const activeBlock = computed(() => {
  return infoBlocks.value.find(block => block.id === activeTabId.value);
});

// Função para mudar a aba ativa
const selectTab = (id) => {
  activeTabId.value = id;
};
</script>

<template>
  <section id="about" class="about">
    <div class="container">
      <div class="logo">
        <a href="#hero"><img src="../assets/images/LogoTestFy-removebg-final.png" alt="Testfy Logo" class="logo-image" /></a>
      </div>
      <h2>Quem Somos...</h2>

      <div class="tab-navigation">
        <button
          v-for="tab in infoBlocks"
          :key="tab.id"
          @click="selectTab(tab.id)"
          :class="{ active: activeTabId === tab.id }"
          class="tab-button"
        >
          {{ tab.title }}
        </button>
      </div>

      <div class="tab-content-wrapper">
        <transition name="fade-slide" mode="out-in">
          <div :key="activeBlock.id" class="info-block-single">
            <div class="block-image-container">
              <img
                :src="activeBlock.image"
                :alt="activeBlock.title"
                class="block-image"
                loading="lazy"
              />
            </div>

            <div class="block-text-content">
              <h3>{{ activeBlock.title }}</h3>
              <p v-for="(paragraph, index) in activeBlock.content" :key="index">
                {{ paragraph }}
              </p>
            </div>
          </div>
        </transition>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
  padding: var(--spacing-lg) var(--spacing-md);
  background-color: var(--color-white);
  color: var(--color-dark);
}

.about h2 {
  text-align: center;
  font-size: var(--font-size-xl);
  margin-bottom: var(--spacing-lg);
  color: var(--color-primary);
}

.logo {
  display: flex;
  justify-content: center;
  margin-bottom: var(--spacing-md);
}

.logo-image {
  max-height: 80px;
  width: auto;
}

.tab-navigation {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: var(--spacing-sm);
  margin-bottom: var(--spacing-lg);
  border-bottom: 2px solid var(--color-light);
  padding-bottom: var(--spacing-xs);
}

.tab-button {
  background-color: transparent;
  border: none;
  padding: var(--spacing-xs) var(--spacing-md);
  font-size: var(--font-size-md);
  font-weight: 600;
  color: var(--color-dark);
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  text-align: center;
  white-space: nowrap;
}

.tab-button:hover {
  color: var(--color-primary);
}

.tab-button.active {
  color: var(--color-primary);
}

.tab-button.active::after {
  content: '';
  position: absolute;
  left: 0;
  right: 0;
  bottom: -2px;
  height: 3px;
  background-color: var(--color-primary);
  border-radius: 2px;
}

.tab-content-wrapper {
  min-height: 350px;
  display: flex;
  justify-content: center;
}

.info-block-single {
  background-color: var(--color-light);
  border-radius: 8px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  padding: var(--spacing-lg);
  max-width: 800px;
  width: 100%;
  text-align: left; /* Padrão para o texto */

  /* Por padrão (mobile-first), o display é column para mobile */
  display: flex;
  flex-direction: column;
  align-items: center; /* Centraliza a imagem e o bloco de texto */
}

/* Esconde a imagem por padrão (mobile-first) */
.block-image-container {
  display: none;
}

.block-image {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain; /* Garante que a imagem se ajuste sem cortar */
  display: block; /* Garante que a imagem se comporte como um bloco */
}

.block-text-content {
  flex: 1; /* Permite que o conteúdo de texto ocupe o espaço restante */
  width: 100%; /* Garante que o texto ocupe a largura disponível em mobile */
}

.info-block-single h3 {
  font-size: var(--font-size-lg);
  color: var(--color-primary);
  margin-bottom: var(--spacing-md);
  text-align: center; /* Centralizado em mobile */
  position: relative;
  padding-bottom: var(--spacing-xs);
}

.info-block-single h3::after {
  content: '';
  position: absolute;
  left: 50%; /* Centraliza a linha em mobile */
  transform: translateX(-50%);
  bottom: 0;
  width: 50px;
  height: 3px;
  background-color: var(--color-primary);
  border-radius: 2px;
}

.info-block-single p {
  font-size: var(--font-size-base);
  line-height: 1.7;
  margin-bottom: var(--spacing-sm);
  color: var(--color-dark);
}

/* Estilos para a transição */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.5s ease-in-out;
}

.fade-slide-enter-from {
  opacity: 0;
  transform: translateX(-20px);
}

.fade-slide-leave-to {
  opacity: 0;
  transform: translateX(20px);
}

/* Media Queries para responsividade */
/* Breakpoint para desktop */
@media (min-width: 769px) {
  .info-block-single {
    flex-direction: row; /* Imagem e texto lado a lado */
    align-items: flex-start; /* Alinha os itens ao topo */
  }

  .block-image-container {
    display: flex; /* Torna a imagem visível no desktop */
    width: 50%; /* Largura fixa para o container da imagem */
    height: 100%; /* Altura fixa para o container da imagem */
    flex-shrink: 0; /* Impede que o container da imagem encolha */
    margin-right: var(--spacing-lg); /* Espaçamento entre imagem e texto */
  }

  .info-block-single h3 {
    text-align: left; /* Alinha o título à esquerda no desktop */
  }
  .info-block-single h3::after {
    left: 0; /* Alinha a linha à esquerda no desktop */
    transform: translateX(0);
  }
}

/* Media Query para telas menores (mobile) */
@media (max-width: 768px) {
  .about {
    padding: var(--spacing-md) var(--spacing-sm);
  }

  .about h2 {
    font-size: var(--font-size-xl);
    margin-bottom: var(--spacing-md);
  }

  .tab-navigation {
    flex-direction: column;
    gap: var(--spacing-xs);
    border-bottom: none;
    margin-bottom: var(--spacing-md);
  }

  .tab-button {
    width: 100%;
    padding: var(--spacing-sm) var(--spacing-xs);
    font-size: var(--font-size-sm);
    border-radius: 4px;
    background-color: var(--color-light-alt);
  }

  .tab-button.active {
    background-color: var(--color-primary-light);
    color: var(--color-primary-dark);
  }

  .tab-button.active::after {
    display: none;
  }

  .info-block-single {
    padding: var(--spacing-md) var(--spacing-sm);
  }

  .info-block-single p {
    font-size: var(--font-size-sm);
  }
  /* O block-image-container já está com display: none por padrão (mobile-first) */
}
</style>
