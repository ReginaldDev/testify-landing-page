<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const isMobileMenuOpen = ref(false);
const isHeaderVisible = ref(true);

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value;
};

let lastScrollY = window.scrollY;
let lastMouseY = 0;

const isMobile = () => window.innerWidth <= 768;

const handleScroll = () => {
  const currentScrollY = window.scrollY;

  if (isMobile()) {
    if (currentScrollY < lastScrollY) {
      isHeaderVisible.value = true; // Rolando pra cima → mostra
    } else if (currentScrollY > lastScrollY + 10) {
      isHeaderVisible.value = false; // Rolando pra baixo → esconde
    }
  }

  lastScrollY = currentScrollY;
};

const handleMouseMove = (event) => {
  if (!isMobile()) {
    const y = event.clientY;

    if (y <= 50) {
      isHeaderVisible.value = true;
    } else if (y > 100 && y > lastMouseY) {
      isHeaderVisible.value = false;
    }

    lastMouseY = y;
  }
};

onMounted(() => {
  window.addEventListener('mousemove', handleMouseMove);
  window.addEventListener('scroll', handleScroll);
});

onBeforeUnmount(() => {
  window.removeEventListener('mousemove', handleMouseMove);
  window.removeEventListener('scroll', handleScroll);
});
</script>

<template>
  <header class="header" :class="{ 'hidden-header': !isHeaderVisible }">
    <div class="logo">
      <a href="#hero"><img src="../assets/images/LogoTestFy-removebg-final - light.png" alt="Testify Logo" class="logo-image" /></a>
    </div>
    <nav :class="{ 'nav-open': isMobileMenuOpen }">
      <div class="mobile-menu-logo">
        <img src="../assets/images/LogoTestFy-removebg-final - light.png" alt="Testify Logo" class="logo-image"/>
      </div>
      <ul class="nav-list">
        <li><a href="#about" @click="isMobileMenuOpen = false" class="nav-link">Sobre</a></li>
        <li><a href="#benefits" @click="isMobileMenuOpen = false" class="nav-link">Benefícios</a></li>
        <li><a href="#technologies" @click="isMobileMenuOpen = false" class="nav-link">Tecnologias</a></li>
        <li><a href="#services" @click="isMobileMenuOpen = false" class="nav-link">Serviços</a></li>
        <li><a href="#contact" @click="isMobileMenuOpen = false" class="nav-link">Contato</a></li>
      </ul>
    </nav>
    <button class="menu-toggle" @click="toggleMobileMenu" :class="{ 'active': isMobileMenuOpen }" aria-label="Abrir menu de navegação">
      <span class="bar"></span>
      <span class="bar"></span>
      <span class="bar"></span>
    </button>
  </header>
</template>

<style scoped>
/* Estilos existentes do .header, .logo, .logo-image, .logo span, .nav-list, .nav-link permanecem os mesmos */

.header {
  background-color: var(--color-dark);
  color: var(--color-white);
  padding: var(--spacing-sm) var(--spacing-md);
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 80px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  z-index: 1000;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  display: flex;
  align-items: center;
}

.logo-image {
  height: 80px; /* Ajuste conforme o tamanho real do seu logo */
  margin-right: var(--spacing-xs);
}

.logo span {
  font-size: var(--font-size-lg);
  font-weight: bold;
  color: var(--color-white);
}

.nav-list {
  list-style: none;
  display: flex;
  gap: var(--spacing-md);
}

.nav-link {
  padding: var(--spacing-xs) var(--spacing-sm);
  text-decoration: none;
  color: var(--color-white);
  font-weight: 500;
  transition: all 0.3s ease;
  border-radius: 4px;
  font-size: var(--font-size-base);
}

.nav-link:hover {
  background-color: rgba(255, 255, 255, 0.1);
  color: var(--color-primary);
}

/* Estilos para o menu hambúrguer (mobile) */
.menu-toggle {
  display: none; /* Esconde por padrão em desktop */
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
  flex-direction: column;
  justify-content: space-around;
  width: 30px;
  height: 25px;
  z-index: 1001;
}

.menu-toggle .bar {
  width: 100%;
  height: 3px;
  background-color: var(--color-white);
  border-radius: 2px;
  transition: all 0.3s ease;
}

/* Estilos para o logo no menu mobile e botão de fechar */
.mobile-menu-logo {
  display: none; /* Esconde por padrão */
  position: absolute; /* Posição absoluta para ficar no topo */
  top: var(--spacing-md);
  left: var(--spacing-md);
  align-items: center;
  font-size: var(--font-size-lg);
  font-weight: bold;
  color: var(--color-white);
}

.mobile-menu-logo .logo-image {
  height: 80px; /* Ligeiramente maior no menu mobile, se desejar */
}

.close-menu-toggle {
  display: none; /* Esconde por padrão */
  background: none;
  border: none;
  color: var(--color-white);
  font-size: 2rem; /* Tamanho do 'X' */
  cursor: pointer;
  position: absolute;
  top: var(--spacing-sm);
  right: var(--spacing-md);
  z-index: 1002; /* Acima de tudo no menu mobile */
  padding: 0.5rem;
}

/* Media query para telas menores (mobile) */
@media (max-width: 768px) {
  .menu-toggle {
    display: flex; /* Mostra o hambúrguer em mobile */
  }

  nav {
    display: none; /* Esconde a navegação padrão em mobile */
    flex-direction: column;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background-color: var(--color-dark);
    padding-top: 80px; /* Mais espaço para o logo e botão de fechar */
    align-items: center;
    justify-content: center;
    z-index: 999;
    transition: transform 0.3s ease-in-out;
    transform: translateX(100%);
  }

  .nav-open {
    display: flex;
    transform: translateX(0);
  }

  .mobile-menu-logo {
    display: flex; /* Mostra o logo no menu mobile quando ativo */
  }

  .close-menu-toggle {
    display: block; /* Mostra o botão de fechar no menu mobile */
  }

  .nav-list {
    flex-direction: column;
    align-items: center;
    gap: var(--spacing-lg);
    margin-top: var(--spacing-lg); /* Espaço entre logo e itens do menu */
  }

  .nav-list li {
    margin: 0;
  }

  .nav-link {
    font-size: var(--font-size-xl);
    padding: var(--spacing-sm) var(--spacing-lg);
  }

  /* Animação do botão hambúrguer para 'X' */
  .menu-toggle.active .bar:nth-child(1) {
    transform: translateY(11px) rotate(45deg);
  }
  .menu-toggle.active .bar:nth-child(2) {
    opacity: 0;
  }
  .menu-toggle.active .bar:nth-child(3) {
    transform: translateY(-11px) rotate(-45deg);
  }
}

.hidden-header {
  transform: translateY(-100%);
  transition: transform 0.4s ease-in-out;
}

.header {
  transition: transform 0.4s ease-in-out;
}
</style>
