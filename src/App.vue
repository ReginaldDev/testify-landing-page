<script setup>
// Aqui vamos importar nossos componentes no futuro
import { ref, onMounted } from 'vue'; // Importe 'ref' e 'onMounted'
import TheHeader from './components/TheHeader.vue';
import HeroSection from './components/HeroSection.vue';
import ServicesSection from './components/ServicesSection.vue';
import BenefitsSection from './components/BenefitsSection.vue';
import WhyUsSection from './components/WhyUsSection.vue';
import TechnologiesSection from './components/TechnologiesSection.vue';
import ContactSection from './components/ContactSection.vue';
import TheFooter from './components/TheFooter.vue';

const showSuccessMessage = ref(false); // Variável reativa para controlar a visibilidade da mensagem

onMounted(() => {
  // Verifica se a URL contém o parâmetro '?sent=true' após o hash
  // Ex: http://localhost:5173/#contact?sent=true
  const urlParams = new URLSearchParams(window.location.hash.split('?')[1]);
  if (urlParams.get('sent') === 'true') {
    showSuccessMessage.value = true;
    // Opcional: remover o parâmetro da URL para não aparecer no refresh manual
    window.history.replaceState({}, document.title, window.location.pathname + window.location.hash.split('?')[0]);

    // Esconde a mensagem após alguns segundos (ex: 5 segundos)
    setTimeout(() => {
      showSuccessMessage.value = false;
    }, 5000);
  }
});
</script>

<template>
  <TheHeader />

  <main>
    <div v-if="showSuccessMessage" class="success-message">
      <p>Sua mensagem foi enviada com sucesso! Em breve entraremos em contato.</p>
      <button @click="showSuccessMessage = false" class="close-message">X</button>
    </div>

    <HeroSection />
    <ServicesSection />
    <BenefitsSection />
    <WhyUsSection />
    <TechnologiesSection />
    <ContactSection />
  </main>

  <TheFooter />
</template>

<style>

</style>
