<script setup>
import { ref, onMounted } from 'vue';
import { animate, stagger } from "motion";
import { splitText } from "motion-plus";

const heroContentRef = ref(null);

onMounted(() => {
  if (!heroContentRef.value) return;

  const h1Element = heroContentRef.value.querySelector("h1");
  h1Element.style.opacity = '1';

  const { words } = splitText(h1Element);
  words.forEach(word => word.style.opacity = '0');

  animate(
    words,
    { opacity: [0, 1], y: [10, 0] },
    {
      type: "spring",
      duration: 2,
      bounce: 0.25,
      delay: stagger(0.05),
    }
  );

  const pElement = heroContentRef.value.querySelector("p");
  const ctaButtonElement = heroContentRef.value.querySelector(".cta-button");

  pElement.style.opacity = '0';
  ctaButtonElement.style.opacity = '0';

  animate(
    [pElement, ctaButtonElement],
    { opacity: [0, 1], y: [10, 0] },
    {
      duration: 2,
      delay: 0.8,
      type: "spring",
      bounce: 0.35,
    }
  );
});
</script>

<template>
  <section id="hero" class="hero">
    <video autoplay loop muted playsinline class="background-video">
      <source src="../assets/videos/video1.mp4" type="video/mp4">
      <!-- <source src="/videos/background-video.webm" type="video/webm"> -->
      Seu navegador não suporta a tag de vídeo.
    </video>

    <div class="video-overlay"></div>

    <div class="hero-content" ref="heroContentRef">
      <h1>Testes Inteligentes. Software Robusto.</h1>
      <p>Deixe os bugs conosco. Você foca no que realmente importa: crescer.</p>
      <a href="#contact" class="cta-button">Fale com a Testfy</a>
    </div>
  </section>
</template>

<style scoped>
.hero {
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  height: 100vh;
  padding: 0 var(--spacing-md);
  /* Remova o background gradiente, o vídeo será o fundo */
  /* background: linear-gradient(133deg,rgba(13, 110, 253, 1) 0%, rgba(7, 151, 176, 1) 50%, rgba(13, 202, 240, 1) 100%); */

  color: var(--color-white); /* Cor do texto principal */
  position: relative; /* Necessário para posicionar o vídeo e o overlay absolutamente */
  overflow: hidden; /* Garante que o vídeo não "vaze" para fora da seção */
}

.background-video {
  position: absolute;
  top: 0;
  left: 0;
  /* min-width: 100%; */
  /* min-height: 100%; */
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: 1; /* Vídeo no fundo, mas acima do background 'real' da section */
  /* transform: translateX(-50%) translateY(-50%); Centraliza o vídeo */
  background-size: cover; /* Garante que o vídeo cubra a área sem distorcer */
}

.video-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5); /* Camada preta semi-transparente (50% opacidade) */
  z-index: 2; /* Acima do vídeo, abaixo do conteúdo */
}

.hero-content {
  max-width: 800px;
  padding: var(--spacing-md);
  position: relative; /* Necessário para que o conteúdo fique acima do overlay */
  z-index: 3; /* Acima do vídeo e do overlay */
}

.hero-content h1 {
  font-size: var(--font-size-xxl);
  font-weight: bold;
  margin-bottom: var(--spacing-sm);
  color: var(--color-white);
  text-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);
}

.split-word {
  will-change: transform, opacity;
  display: inline-block;
}

.hero-content p {
  font-size: var(--font-size-md);
  max-width: 600px;
  margin: 0 auto var(--spacing-md) auto;
  color: var(--color-light); /* Pode precisar ser var(--color-white) se a overlay for muito escura */
  text-shadow: 3px 3px 5px rgba(0, 0, 0, 0.5);
}

.cta-button {
  display: inline-block;
  background-color: var(--color-transparent);
  color: var(--color-white);
  padding: var(--spacing-sm) var(--spacing-md);
  border-radius: 5px;
  border: solid 1px;
  text-decoration: none;
  font-size: var(--font-size-md);
  font-weight: bold;
  transition: all 0.3s ease;
  box-shadow: 3px 3px 10px rgba(0, 0, 0, 0.3);
}

.cta-button:hover {
  background-color: color-mix(in srgb, var(--color-transparent) 90%, rgb(245, 245, 245));
  box-shadow:  3px 3px 10px rgba(250, 248, 248, 0.753);
}

@media (max-width: 768px) {
  .hero-content h1 {
    font-size: var(--font-size-xl);
  }
  .hero-content p {
    font-size: var(--font-size-base);
  }
  /* Em mobile, considere usar uma imagem de fallback ou simplificar o vídeo */
  /* .background-video { */
    /* display: none; Esconde o vídeo em mobile para economizar dados e bateria */
  /* } */
  .hero {
    /* Adicione uma imagem de fallback ou um fundo sólido para mobile */
    background-image: url('/images/hero-fallback.jpg'); /* Crie esta imagem na pasta public/images */
    background-size: cover;
    background-position: center;
  }
}
</style>
