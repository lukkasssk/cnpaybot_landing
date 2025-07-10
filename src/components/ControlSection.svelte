<script>
  import { onMount } from 'svelte'
  import { fly, fade } from 'svelte/transition'
</script>

<section class="control-section">
  <div class="container">
    <div class="content" in:fly={{ y: 50, duration: 800 }}>
      <h2 class="title">
        Controle <span class="highlight">Total</span> na Palma da mão
      </h2>
      <p class="description">
        Ação nativa com todas as funcionalidades do dashboard. Monitore vendas, receba notificações e gerencie seu negócio de qualquer lugar.
      </p>
    </div>
    
    <div class="image-container" in:fly={{ y: 50, duration: 800, delay: 200 }}>
      <img 
        alt="Dashboard de controle" 
        class="dashboard-image" 
        src="../static/imagem/cnpay.png"
      />
    </div>
  </div>
</section>

<style>
  .control-section {
    border-radius: 30px 30px 0 0;
    padding: 3rem 1rem;
    background: white;
  }

  .container {
    max-width: 1400px;
    margin: 0 auto;
    text-align: center;
    width: 100%;
  }

  .content {
    margin-bottom: 3rem;
  }

  .title {
    font-size: 2rem;
    font-weight: 700;
    margin-bottom: 1.5rem;
    color: #1f2937;
  }

  .highlight {
    color: #0088cc;
  }

  .description {
    font-size: 1.25rem;
    color: #6b7280;
    max-width: 64rem;
    margin: 0 auto;
    line-height: 1.6;
    font-weight: 500;
  }

  .image-container {
    margin-top: 3rem;
  }

  .dashboard-image {
    width: 100%;
    max-width: 800px;
    height: auto;
    border-radius: 8px;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
    border: 1px solid #e5e7eb;
    transition: all 0.3s ease;
  }

  .dashboard-image:hover {
    transform: translateY(-4px);
    box-shadow: 0 10px 25px -3px rgba(0, 0, 0, 0.1);
  }

  @media (min-width: 768px) {
    .control-section {
      padding: 5rem 1rem;
    }

    .title {
      font-size: 3rem;
    }

    .description {
      font-size: 1.5rem;
    }
  }

  @media (min-width: 1024px) {
    .title {
      font-size: 3rem;
    }

    .description {
      font-size: 1.75rem;
    }
  }

  @media (min-width: 1280px) {
    .title {
      font-size: 4rem;
    }

    .description {
      font-size: 2rem;
    }
  }
</style> 