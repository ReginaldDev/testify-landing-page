<script setup>
// Aqui está a mágica: guardamos nossos dados em um array de objetos.
// Se precisar adicionar um novo serviço, basta adicioná-lo aqui!
const services = [
  {
    title: 'Testes Funcionais e Não Funcionais',
    description: 'Garantimos que cada funcionalidade do seu software opere conforme o esperado, identificando bugs antes que cheguem ao usuário.'
  },
  {
    title: 'Testes para Web e Mobile',
    description: 'Verificamos as funcionalidades e usabilidade do seu site ou aplicativo.'
  },
  {
    title: 'Testes de Performance',
    description: 'Avaliamos a velocidade, responsividade e estabilidade do seu sistema sob diferentes cargas de trabalho.'
  },
  {
    title: 'Automação de Testes',
    description: 'Desenvolvemos scripts de automação para acelerar o ciclo de testes, aumentar a cobertura e reduzir custos operacionais.'
  },
  {
    title: 'Testes para API',
    description: 'Verificamos a comunicação eficiente entre sistemas.'
  },
  {
    title: 'Consultoria em QA',
    description: 'Oferecemos nossa expertise para ajudar sua equipe a implementar as melhores práticas e processos de Qualidade de Software.'
  }
]
</script>

<template>
  <section id="services" class="services">
    <div class="container">
      <h2>Nossos Serviços</h2>
      <div class="services-grid">
        <article v-for="service in services" :key="service.title" class="service-card">
          <h3>{{ service.title }}</h3>
          <p>{{ service.description }}</p>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.services {
  padding: var(--spacing-lg) var(--spacing-md); /* Usando variáveis para padding */
  background-color: var(--color-white); /* Usando variável */
  color: var(--color-dark); /* Adicionado para garantir a cor do texto principal */
}

/* O .container aqui pode ser removido, já que você tem um .container global em main.css
   que já faz a centralização e padding. Se você tiver um div com classe `container`
   dentro do template desta seção, ele já pegará os estilos globais. */
/* .container {
   max-width: var(--max-width-desktop, 1120px);
   margin: 0 auto;
} */

.services h2 {
  text-align: center;
  font-size: var(--font-size-xl); /* Usando variável para o título da seção */
  margin-bottom: var(--spacing-lg); /* Usando variável para espaçamento */
  color: var(--color-dark); /* Usando variável */
}

.services-grid {
  display: grid;
  /* Cria um grid responsivo: 2 colunas em telas maiores, 1 em menores */
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: var(--spacing-md); /* Usando variável para o espaçamento entre cards */
}

.service-card {
  background-color: var(--color-light); /* Usando variável */
  padding: var(--spacing-md); /* Usando variável */
  border-radius: 8px;
  box-shadow: 0 4px 15px #09000f41;
  border: 1px solid #eaeaea; /* Mantenho fixo se não tiver uma variável para bordas muito claras */
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.service-card:hover {
  transform: translateY(-5px); /* Efeito de levantar o card */
  box-shadow: 0 4px 20px #9000ff54; /* Sombra suave */
}

.service-card h3 {
  font-size: var(--font-size-lg); /* Usando variável para o título do card */
  margin-bottom: var(--spacing-sm); /* Usando variável */
  color: var(--color-primary); /* Usando variável */
}

.service-card p {
  color: var(--color-dark); /* Garante que o texto do parágrafo use a cor padrão */
  font-size: var(--font-size-base); /* Tamanho de fonte padrão */
}

/* Media query para ajustar o tamanho do título da seção em telas menores */
@media (max-width: 768px) {
  .services h2 {
    font-size: var(--font-size-xl); /* Mantém um bom tamanho em mobile */
    margin-bottom: var(--spacing-md); /* Ajusta espaçamento */
  }
  .services-grid {
    gap: var(--spacing-sm); /* Reduz espaçamento entre cards em mobile, se desejar */
  }
}
</style>
