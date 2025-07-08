<script>
  import { onMount } from 'svelte';
  import { fly, fade } from 'svelte/transition';

  let email = '';
  let isSubmitting = false;
  let submitted = false;

  function handleSubmit() {
    if (!email) return;
    
    isSubmitting = true;
    
    // Simular envio
    setTimeout(() => {
      isSubmitting = false;
      submitted = true;
      email = '';
      
      // Reset após 3 segundos
      setTimeout(() => {
        submitted = false;
      }, 3000);
    }, 1000);
  }

  function scrollToPricing() {
    const element = document.getElementById('pricing');
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' });
    }
  }
</script>

<section class="cta" id="cta">
  <div class="container">
    <div class="cta-content" in:fly={{ y: 50, duration: 800 }}>
      <h2>Pronto para monetizar sua comunidade?</h2>
      <p>Junte-se a milhares de criadores que já transformaram suas comunidades em fontes de renda consistentes</p>
      
      <div class="cta-buttons">
        <button class="btn-primary" on:click={scrollToPricing}>
          Começar Agora
        </button>
        <button class="btn-outline">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
            <path d="M8 5v14l11-7z" fill="currentColor"/>
          </svg>
          CRIAR MEU BOT
        </button>
      </div>
    </div>

    <div class="newsletter-section" in:fade={{ duration: 800, delay: 400 }}>
      <div class="newsletter-content">
        <h3>Receba dicas exclusivas</h3>
        <p>Inscreva-se para receber estratégias de monetização e novidades da plataforma</p>
        
        <form class="newsletter-form" on:submit|preventDefault={handleSubmit}>
          <div class="input-group">
            <input 
              type="email" 
              placeholder="Seu melhor email"
              bind:value={email}
              required
              disabled={isSubmitting}
            />
            <button type="submit" disabled={isSubmitting || !email}>
              {#if isSubmitting}
                <svg class="spinner" width="20" height="20" viewBox="0 0 24 24" fill="none">
                  <path d="M12 2v4m0 12v4m4.95-11.95l-2.83 2.83M5.05 5.05l2.83 2.83" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
              {:else}
                Inscrever
              {/if}
            </button>
          </div>
          
          {#if submitted}
            <div class="success-message" in:fly={{ y: 20, duration: 300 }}>
              ✅ Email cadastrado com sucesso!
            </div>
          {/if}
        </form>
      </div>
    </div>

    <div class="benefits-grid" in:fly={{ y: 50, duration: 800, delay: 600 }}>
      <div class="benefit-item">
        <div class="benefit-icon">🚀</div>
        <h4>Setup em 5 minutos</h4>
        <p>Configure sua comunidade e comece a vender rapidamente</p>
      </div>
      
      <div class="benefit-item">
        <div class="benefit-icon">💰</div>
        <h4>Sem taxas ocultas</h4>
        <p>Preços transparentes, sem surpresas</p>
      </div>
      
      <div class="benefit-item">
        <div class="benefit-icon">🛡️</div>
        <h4>Segurança garantida</h4>
        <p>Seus dados e pagamentos protegidos</p>
      </div>
      
      <div class="benefit-item">
        <div class="benefit-icon">📱</div>
        <h4>Suporte 24/7</h4>
        <p>Estamos sempre aqui para ajudar</p>
      </div>
    </div>
  </div>
</section>

<style>
  .cta {
    padding: 6rem 2rem;
    background: transparent;
    color: white;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
  }

  .cta-content {
    text-align: center;
    margin-bottom: 4rem;
  }

  .cta-content h2 {
    font-size: 3rem;
    font-weight: 700;
    margin-bottom: 1.5rem;
    background: linear-gradient(135deg, #ffffff, #e5e7eb);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .cta-content p {
    font-size: 1.25rem;
    color: #d1d5db;
    max-width: 600px;
    margin: 0 auto 2rem;
    line-height: 1.6;
  }

  .cta-buttons {
    display: flex;
    gap: 1rem;
    justify-content: center;
    flex-wrap: wrap;
  }

  .btn-primary {
    background: linear-gradient(135deg, #0088cc, #1cb1ff);
    color: black;
    border: none;
    padding: 1.3rem 3rem;
    border-radius: 30px;
    font-weight: 700;
    font-size: 1.5rem;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: -1px 0px 20px 20px rgba(0, 136, 204, 0.4), 0 4px 15px rgb(0 0 0 / 19%);
    text-transform: uppercase;
    letter-spacing: 2px;
  }

  .btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(0, 136, 204, 0.4);
  }

  .btn-outline {
    background: transparent;
    color: white;
    border: 2px solid #6b7280;
    padding: 1rem 2rem;
    border-radius: 12px;
    font-weight: 600;
    font-size: 1.1rem;
    cursor: pointer;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .btn-outline:hover {
    border-color: #0088cc;
    color: #0088cc;
    transform: translateY(-2px);
  }

  .newsletter-section {
    background: transparent;
    padding: 3rem;
    border-radius: 20px;
    margin-bottom: 4rem;
    backdrop-filter: blur(10px);
  }

  .newsletter-content {
    text-align: center;
    max-width: 500px;
    margin: 0 auto;
  }

  .newsletter-content h3 {
    font-size: 1.75rem;
    font-weight: 600;
    margin-bottom: 1rem;
  }

  .newsletter-content p {
    color: #d1d5db;
    margin-bottom: 2rem;
  }

  .newsletter-form {
    max-width: 400px;
    margin: 0 auto;
  }

  .input-group {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 1rem;
  }

  .input-group input {
    flex: 1;
    padding: 1rem;
    border: 2px solid #4b5563;
    border-radius: 12px;
    background: rgba(255, 255, 255, 0.1);
    color: white;
    font-size: 1rem;
    transition: all 0.3s ease;
  }

  .input-group input::placeholder {
    color: #9ca3af;
  }

  .input-group input:focus {
    outline: none;
    border-color: #0088cc;
    background: rgba(255, 255, 255, 0.15);
  }

  .input-group button {
    padding: 1rem 1.5rem;
    background: linear-gradient(135deg, #0088cc, #00a8ff);
    color: white;
    border: none;
    border-radius: 12px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .input-group button:disabled {
    opacity: 0.6;
    cursor: not-allowed;
  }

  .input-group button:not(:disabled):hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 15px rgba(0, 136, 204, 0.3);
  }

  .spinner {
    animation: spin 1s linear infinite;
  }

  @keyframes spin {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }

  .success-message {
    color: #10b981;
    font-weight: 600;
    text-align: center;
  }

  .benefits-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
  }

  .benefit-item {
    text-align: center;
    padding: 2rem;
    background: rgba(255, 255, 255, 0.05);
    border-radius: 16px;
    backdrop-filter: blur(10px);
    transition: all 0.3s ease;
  }

  .benefit-item:hover {
    transform: translateY(-4px);
    background: rgba(255, 255, 255, 0.1);
  }

  .benefit-icon {
    font-size: 3rem;
    margin-bottom: 1rem;
  }

  .benefit-item h4 {
    font-size: 1.25rem;
    font-weight: 600;
    margin-bottom: 0.5rem;
  }

  .benefit-item p {
    color: #d1d5db;
    font-size: 0.9rem;
  }

  @media (max-width: 768px) {
    .cta {
      padding: 4rem 1rem;
    }

    .cta-content h2 {
      font-size: 2.5rem;
    }

    .cta-content p {
      font-size: 1.1rem;
    }

    .cta-buttons {
      flex-direction: column;
      align-items: center;
    }

    .newsletter-section {
      padding: 2rem;
    }

    .input-group {
      flex-direction: column;
    }

    .benefits-grid {
      grid-template-columns: 1fr;
      gap: 1.5rem;
    }

    .benefit-item {
      padding: 1.5rem;
    }

    .benefit-icon {
      font-size: 2.5rem;
    }
  }
</style> 