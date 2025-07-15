<script setup>
const currentYear = new Date().getFullYear();
</script>

<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-left">
        <a href="#hero" class="logo">
          <img src="../assets/images/LogoTestFy-removebg-final - light.png" alt="Testfy Logo" class="logo-image" />
        </a>
      </div>

      <div class="footer-center">
        <p>&copy; {{ currentYear }} Testfy Brasil. Todos os direitos reservados.</p>
      </div>

      <div class="footer-right">
        <div class="social-links">
          <a href="https://api.whatsapp.com/send?phone=5518991256139" target="_blank" rel="noopener noreferrer" aria-label="Whatsapp">
            <i class="fab fa-whatsapp"></i>
          </a>
          <a href="https://www.linkedin.com/company/testfybr" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn da Testfy">
            <i class="fab fa-linkedin"></i>
          </a>
          <a href="https://www.instagram.com/testfybrasil" target="_blank" rel="noopener noreferrer" aria-label="Instagram da Testfy">
            <i class="fab fa-instagram"></i>
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background-color: var(--color-dark);
  color: var(--color-white);
  padding: var(--spacing-lg) var(--spacing-md); /* Aumenta o padding vertical */
  text-align: center;
  font-size: var(--font-size-sm);
  /* Remover a borda superior para um visual mais limpo */
  border-top: none;
  /* Opcional: adicionar uma sombra sutil no topo para separação */
  box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.2);
}

.container {
  max-width: var(--max-width-desktop, 1120px);
  margin: 0 auto;
  display: flex;
  flex-direction: column; /* Padrão para mobile: empilhado */
  align-items: center; /* Centraliza itens em mobile */
  gap: var(--spacing-md); /* Aumenta o espaço entre os elementos em mobile */
}

/* Nova estrutura de divs para melhor controle do layout */
.footer-left, .footer-center, .footer-right {
  display: flex;
  justify-content: center; /* Centraliza conteúdo dentro de cada div em mobile */
  align-items: center;
  width: 100%; /* Ocupa a largura total em mobile */
}

.logo-image {
  max-height: 50px; /* Ajuste o tamanho da logo, exemplo 50px */
  width: auto;
  margin-bottom: var(--spacing-xs); /* Espaçamento abaixo da logo em mobile */
}

.footer-center p {
    margin: 0; /* Remove margem padrão do parágrafo */
    font-size: var(--font-size-base); /* Tamanho do texto de direitos autorais */
    color: var(--color-light); /* Cor mais suave para o texto de direitos autorais */
}

.social-links {
  display: flex; /* Transforma os links sociais em flex para alinhar horizontalmente */
  gap: var(--spacing-sm); /* Espaçamento entre os ícones */
  margin-top: 0; /* Remover margin-top, o gap do container já cuida disso */
}

.social-links a {
  color: var(--color-white);
  font-size: var(--font-size-xl); /* Ícones um pouco maiores para destaque */
  text-decoration: none;
  transition: color 0.3s ease, transform 0.3s ease; /* Adiciona transição para transform */

  /* Adiciona um fundo sutil aos ícones e um arredondamento */
  background-color: rgba(255, 255, 255, 0.1); /* Fundo branco semi-transparente */
  border-radius: 50%; /* Torna o fundo circular */
  width: 40px; /* Largura do círculo */
  height: 40px; /* Altura do círculo */
  display: flex; /* Para centralizar o ícone dentro do círculo */
  justify-content: center;
  align-items: center;
}

.social-links a:hover {
  color: var(--color-primary);
  background-color: rgba(255, 255, 255, 0.2); /* Fundo um pouco mais opaco no hover */
  transform: translateY(-3px); /* Pequeno efeito de "levantar" no hover */
}

/* Media query para telas maiores: organiza lado a lado */
@media (min-width: 768px) {
  .container {
    flex-direction: row; /* Coloca os itens em linha */
    justify-content: space-between; /* Distribui logo, texto e sociais nas extremidades */
    align-items: center; /* Alinha verticalmente no centro */
    gap: var(--spacing-md); /* Espaçamento entre os blocos em desktop */
  }

  .footer-left, .footer-center, .footer-right {
    width: auto; /* Permite que ocupem apenas o espaço necessário */
    justify-content: flex-start; /* Alinha à esquerda na parte da logo */
  }

  .footer-right {
    justify-content: flex-end; /* Alinha à direita na parte dos sociais */
  }

  .logo-image {
    margin-bottom: 0; /* Remove a margem inferior em desktop */
  }

  .social-links {
    margin-top: 0; /* Remove a margem superior em desktop */
  }
}

/* Ajustes para telas muito pequenas (abaixo de 480px, se necessário) */
@media (max-width: 480px) {
  .footer {
    padding: var(--spacing-md) var(--spacing-sm); /* Reduz padding horizontal em mobile pequeno */
  }
  .logo-image {
    max-height: 40px; /* Logo um pouco menor em telas muito pequenas */
  }
  .social-links a {
    font-size: var(--font-size-lg); /* Ícones um pouco menores */
    width: 35px;
    height: 35px;
  }
}
</style>
