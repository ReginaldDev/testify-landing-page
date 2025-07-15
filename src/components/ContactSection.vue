<script setup>
import { ref } from 'vue';

// Variáveis reativas para os campos do formulário
const name = ref('');
const email = ref('');
const message = ref('');

// Variáveis reativas para controlar o feedback ao usuário
const showSuccessMessage = ref(false);
const showErrorMessage = ref(false);
const submitButtonText = ref('Enviar Mensagem'); // Texto do botão para feedback de carregamento

// SUA CHAVE DE ACESSO DO WEB3FORMS AQUI!
// Substitua 'YOUR_ACCESS_KEY_HERE' pela chave que você obteve no site do Web3Forms.
const WEB3FORMS_ACCESS_KEY = '14f666b8-00e2-43d7-9903-41d034406b50'; // <--- ATUALIZE AQUI!

const handleSubmit = async () => {
  // Resetar mensagens de feedback
  showSuccessMessage.value = false;
  showErrorMessage.value = false;
  submitButtonText.value = 'Enviando...'; // Feedback visual no botão

  // Construir o objeto com os dados do formulário
  const formData = new FormData();
  formData.append('name', name.value);
  formData.append('email', email.value);
  formData.append('message', message.value);
  formData.append('access_key', WEB3FORMS_ACCESS_KEY); // Adiciona a chave de acesso

  // Opcional: Adicionar um assunto ao e-mail no Web3Forms
  // formData.append('subject', 'Nova Mensagem do Site - Testify Brasil');

  try {
    const response = await fetch('https://api.web3forms.com/submit', {
      method: 'POST',
      body: formData, // Envia o FormData
    });

    const data = await response.json(); // Pega a resposta em JSON

    if (data.success) {
      showSuccessMessage.value = true;
      // Limpa os campos do formulário
      name.value = '';
      email.value = '';
      message.value = '';
    } else {
      showErrorMessage.value = true;
      console.error('Erro ao enviar mensagem:', data.message);
    }
  } catch (error) {
    showErrorMessage.value = true;
    console.error('Erro de rede ou ao processar o envio:', error);
  } finally {
    submitButtonText.value = 'Enviar Mensagem'; // Volta ao texto original do botão
    // Esconde as mensagens de feedback após alguns segundos
    setTimeout(() => {
      showSuccessMessage.value = false;
      showErrorMessage.value = false;
    }, 5000);
  }
};
</script>

<template>
  <section id="contact" class="contact">
    <div class="container">
      <h2>Fale Conosco</h2>
      <p class="contact-intro">Envie-nos uma mensagem e descubra como podemos ajudar sua empresa a alcançar a excelência em software.</p>

      <div v-if="showSuccessMessage" class="feedback-message success">
        <p>Sua mensagem foi enviada com sucesso! Em breve entraremos em contato.</p>
      </div>
      <div v-if="showErrorMessage" class="feedback-message error">
        <p>Ocorreu um erro ao enviar sua mensagem. Por favor, tente novamente.</p>
      </div>

      <form @submit.prevent="handleSubmit" class="contact-form">
        <div class="form-group">
          <label for="name">Seu Nome:</label>
          <input type="text" id="name" v-model="name" required>
        </div>
        <div class="form-group">
          <label for="email">Seu E-mail:</label>
          <input type="email" id="email" v-model="email" required>
        </div>
        <div class="form-group">
          <label for="message">Sua Mensagem:</label>
          <textarea id="message" v-model="message" rows="5" required></textarea>
        </div>
        <button type="submit" class="submit-button" :disabled="submitButtonText !== 'Enviar Mensagem'">
          {{ submitButtonText }}
        </button>
      </form>
    </div>
  </section>
</template>

<style scoped>
.contact {
  padding: var(--spacing-lg) var(--spacing-md); /* Usando variáveis para padding */
  background-color: var(--color-white); /* Usando variável */
  color: var(--color-dark); /* Usando variável */
}

.container {
  max-width: 800px; /* Mantém a largura específica para o formulário */
  margin: 0 auto;
}

.contact h2 {
  text-align: center;
  font-size: var(--font-size-xl); /* Usando variável */
  margin-bottom: var(--spacing-sm); /* Usando variável */
  color: var(--color-dark); /* Usando variável */
}

.contact-intro {
  text-align: center;
  font-size: var(--font-size-md); /* Usando variável */
  margin-bottom: var(--spacing-lg); /* Usando variável */
  color: var(--color-secondary); /* Usando variável para cor secundária */
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}

.contact-form {
  background-color: var(--color-light); /* Usando variável para fundo suave */
  padding: var(--spacing-lg); /* Usando variável para padding */
  border-radius: 8px;
  box-shadow: 0 5px 25px rgba(0, 0, 0, 0.1);
}

.form-group {
  margin-bottom: var(--spacing-sm); /* Usando variável */
}

.form-group label {
  display: block;
  margin-bottom: var(--spacing-xs); /* Usando variável */
  font-weight: bold;
  color: var(--color-dark); /* Usando variável */
}

.form-group input[type="text"],
.form-group input[type="email"],
.form-group textarea {
  width: 100%;
  padding: var(--spacing-sm); /* Usando variável */
  border: 1px solid var(--color-secondary-light, #ddd); /* Nova variável ou fallback */
  border-radius: 4px;
  font-size: var(--font-size-base); /* Usando variável */
  transition: border-color 0.3s ease;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--color-primary); /* Usando variável */
  box-shadow: 0 0 0 3px color-mix(in srgb, var(--color-primary) 25%, transparent); /* Sombra mais sutil com a cor primária */
}

.submit-button {
  display: block;
  width: 100%;
  padding: var(--spacing-sm) var(--spacing-md); /* Usando variáveis */
  background-color: var(--color-primary); /* Usando variável */
  color: var(--color-white); /* Usando variável */
  border: none;
  border-radius: 5px;
  font-size: var(--font-size-lg); /* Usando variável */
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.submit-button:hover:not(:disabled) {
  background-color: color-mix(in srgb, var(--color-primary) 80%, black); /* Escurece a cor primária no hover */
}

.submit-button:disabled {
  background-color: var(--color-secondary); /* Usando variável para cor cinza quando desabilitado */
  opacity: 0.7; /* Suaviza um pouco a cor quando desabilitado */
  cursor: not-allowed;
}


/* Estilos para as mensagens de feedback (já estavam usando algumas, agora mais consistentes) */
/* Eu havia sugerido essas classes em main.css para serem globais,
   mas se você preferir mantê-las scoped aqui, também funciona. */
.feedback-message {
  padding: var(--spacing-sm); /* Usando variável */
  margin-bottom: var(--spacing-sm); /* Usando variável */
  border-radius: 5px;
  font-weight: bold;
  text-align: center;
  max-width: 800px; /* Adicionado para limitar a largura se não estiver dentro do container */
  margin-left: auto; /* Centraliza a mensagem */
  margin-right: auto; /* Centraliza a mensagem */
}

.feedback-message.success {
  background-color: var(--color-success-bg, #d4edda); /* Variáveis ou fallback */
  color: var(--color-success-text, #155724);
  border: 1px solid var(--color-success-border, #c3e6cb);
}

.feedback-message.error {
  background-color: var(--color-error-bg, #f8d7da); /* Variáveis ou fallback */
  color: var(--color-error-text, #721c24);
  border: 1px solid var(--color-error-border, #f5c6cb);
}

/* Media Query para telas menores */
@media (max-width: 768px) {
  .contact h2 {
    font-size: var(--font-size-xl); /* Ajusta o tamanho do título da seção para mobile */
  }

  .contact-intro {
    font-size: var(--font-size-base); /* Ajusta o tamanho da introdução para mobile */
    margin-bottom: var(--spacing-md);
  }

  .contact-form {
    padding: var(--spacing-md); /* Reduz o padding do formulário em mobile */
  }

  .form-group label {
    font-size: var(--font-size-base); /* Garante que o label não seja muito pequeno */
  }

  .form-group input,
  .form-group textarea {
    padding: var(--spacing-xs); /* Reduz o padding dos inputs em mobile */
  }

  .submit-button {
    font-size: var(--font-size-md); /* Ajusta o tamanho da fonte do botão em mobile */
    padding: var(--spacing-xs) var(--spacing-sm);
  }
}
</style>
