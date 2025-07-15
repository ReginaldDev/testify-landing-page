<script setup>
// Nenhuma lógica de script complexa necessária aqui.
// Poderíamos ter um array de objetos para as tecnologias,
// mas para simplicidade inicial, vamos hardcodar as imagens.
</script>

<template>
  <section id="technologies" class="technologies">
    <div class="container">
      <h2>Algumas das Tecnologias que Impulsionam Nossos Testes</h2>

      <div class="tech-logos">
        <div class="tech-item">
          <img src="../assets/images/technologies/cypress.png" alt="Cypress Logo" loading="lazy">
          <span>Cypress</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/robotframework.png" alt="Robot Framework Logo" loading="lazy">
          <span>Robot Framework</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/selenium.png" alt="Selenium Logo" loading="lazy">
          <span>Selenium</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/playwright.png" alt="Playwright Logo" loading="lazy">
          <span>Playwright</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/k6.png" alt="k6 Logo" loading="lazy">
          <span>k6</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/postman.png" alt="Postman Logo" loading="lazy">
          <span>Postman</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/jmeter.png" alt="JMeter Logo" loading="lazy">
          <span>JMeter</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/owasp.png" alt="OWASP ZAP Logo" loading="lazy">
          <span>OWASP ZAP</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/bugzilla.png" alt="Bugzilla Logo" loading="lazy">
          <span>Bugzilla</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/testrail.png" alt="TestRail Logo" loading="lazy">
          <span>TestRail</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/github.png" alt="Github Logo" loading="lazy">
          <span>GitHub</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/swagger.png" alt="Swagger Logo" loading="lazy">
          <span>Swagger</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/javascript.png" alt="Javascript Logo" loading="lazy">
          <span>Javascript</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/python.png" alt="Python Logo" loading="lazy">
          <span>Python</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/docker.png" alt="Docker Logo" loading="lazy">
          <span>Docker</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/jenkins.png" alt="Jenkins Logo" loading="lazy">
          <span>Jenkins</span>
        </div>
        <div class="tech-item">
          <img src="../assets/images/technologies/jira.png" alt="Jira Logo" loading="lazy">
          <span>Jira</span>
        </div>
        <div class="tech-item">
          <p>E outras mais...</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.technologies {
  padding: var(--spacing-lg) var(--spacing-md);
  background-color: var(--color-light); /* Um fundo mais claro para contrastar com as seções adjacentes */
  color: var(--color-dark);
  text-align: center;
}

.technologies h2 {
  font-size: var(--font-size-xl);
  margin-bottom: var(--spacing-lg);
  color: var(--color-primary);
}

.tech-logos {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr)); /* Layout de grade responsivo */
  gap: var(--spacing-md); /* Espaçamento entre as logos */
  justify-items: center; /* Centraliza itens na célula da grade */
  align-items: center; /* Alinha itens verticalmente no centro da célula */
}

.tech-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: var(--spacing-sm);
  background-color: var(--color-white); /* Fundo branco para cada item da logo */
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease; /* Efeito hover sutil */
  height: 150px; /* Altura fixa para os cards da logo */
  width: 100%; /* Ocupa a largura da célula da grade */
  max-width: 150px; /* Limita a largura máxima do item para não ficarem muito grandes */
  text-align: center;
}

.tech-item:hover {
  transform: translateY(-5px); /* Levanta o card no hover */
}

.tech-item img {
  max-width: 80px; /* Tamanho máximo da logo dentro do card */
  max-height: 80px; /* Altura máxima da logo */
  height: auto;
  margin-bottom: var(--spacing-xs); /* Espaçamento entre logo e texto */
}

.tech-item span {
  font-size: var(--font-size-sm);
  color: var(--color-dark);
  font-weight: 600;
  text-align: center;
  word-break: break-word; /* Garante que o texto quebre se for muito longo */
}

/* Media Queries para responsividade */
@media (max-width: 768px) {
  .technologies h2 {
    font-size: var(--font-size-xl);
    margin-bottom: var(--spacing-md);
  }
  .tech-logos {
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr)); /* Colunas menores em mobile */
    gap: var(--spacing-sm);
  }
  .tech-item {
    height: 120px; /* Altura menor para cards em mobile */
    max-width: 120px;
    padding: var(--spacing-xs);
  }
  .tech-item img {
    max-width: 60px;
    max-height: 60px;
  }
  .tech-item span {
    display: none;
    /* font-size: var(--font-size-xs);  */
  }
}

@media (max-width: 480px) {
  .tech-logos {
    grid-template-columns: repeat(auto-fit, minmax(80px, 1fr)); /* Ainda menores em telas muito pequenas */
  }
  .tech-item {
    height: 100px;
    max-width: 100px;
  }
  .tech-item img {
    max-width: 50px;
    max-height: 50px;
  }
}
</style>
