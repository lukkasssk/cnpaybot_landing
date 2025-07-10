<script>
  function scrollToSection(sectionId) {
    const element = document.getElementById(sectionId);
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' });
    }
  }
</script>

<footer class="footer">
  <div class="container">
    <div class="footer-grid">
      <div class="footer-main">
        <div class="logo-section">
          <img alt="CN Bot Logo" class="logo" src="/static/imagem/cnbot_logo_branco.png">
        </div>
        <p class="description">
          A plataforma mais completa para automatizar vendas de assinaturas no Telegram. Transforme seu conteúdo em uma fonte de renda recorrente.
        </p>
        <div class="social-buttons">
          <button class="social-btn">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="icon">
              <path d="M7.9 20A9 9 0 1 0 4 16.1L2 22Z"></path>
            </svg>
            Telegram
          </button>
          <button class="social-btn">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="icon">
              <circle cx="12" cy="12" r="10"></circle>
              <path d="M12 2a14.5 14.5 0 0 0 0 20 14.5 14.5 0 0 0 0-20"></path>
              <path d="M2 12h20"></path>
            </svg>
            Site
          </button>
        </div>
      </div>
      
      <div class="footer-links">
        <h3>Links Rápidos</h3>
        <ul>
          <li><button on:click={() => scrollToSection('features')}>Funcionalidades</button></li>
          <li><button on:click={() => scrollToSection('how-it-works')}>Como Funciona</button></li>
          <li><button on:click={() => scrollToSection('features')}>Benefícios</button></li>
          <li><button on:click={() => scrollToSection('pricing')}>Preços</button></li>
        </ul>
      </div>
      
      <div class="footer-links">
        <h3>Suporte</h3>
        <ul>
          <li><a href="#">Central de Ajuda</a></li>
          <li><a href="#">Documentação</a></li>
          <li><a href="#">Contato</a></li>
          <li><a href="#">Status do Sistema</a></li>
        </ul>
      </div>
    </div>
    
    <div class="footer-bottom">
      <p class="copyright">© 2024 CN Bot. Todos os direitos reservados.</p>
      <div class="legal-links">
        <a href="#">Termos de Uso</a>
        <a href="#">Política de Privacidade</a>
      </div>
    </div>
  </div>
</footer>

<style>
  .footer {
    background: #1e293b;
    color: white;
    padding: 3rem 1rem;
  }

  .container {
    max-width: 1400px;
    margin: 0 auto;
    padding: 0 1rem;
  }

  .footer-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .footer-main {
    grid-column: span 1;
  }

  .logo-section {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    margin-bottom: 1.5rem;
  }

  .logo {
    height: 3rem;
    width: auto;
    object-fit: contain;
  }

  .description {
    color: #cbd5e1;
    font-size: 1.125rem;
    line-height: 1.6;
    margin-bottom: 1.5rem;
  }

  .social-buttons {
    display: flex;
    gap: 1rem;
  }

  .social-btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    white-space: nowrap;
    font-size: 0.875rem;
    font-weight: 500;
    transition: all 0.3s ease;
    border: 1px solid #475569;
    background: transparent;
    color: #cbd5e1;
    height: 2rem;
    border-radius: 0.375rem;
    gap: 0.375rem;
    padding: 0 0.75rem;
    cursor: pointer;
  }

  .social-btn:hover {
    background: #334155;
    color: white;
  }

  .icon {
    width: 1rem;
    height: 1rem;
  }

  .footer-links h3 {
    font-size: 1.25rem;
    font-weight: 700;
    margin-bottom: 1.5rem;
  }

  .footer-links ul {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }

  .footer-links  ul li{
    list-style: none;
  }

  .footer-links li button,
  .footer-links li a {
    color: #cbd5e1;
    transition: color 0.3s ease;
    background: none;
    border: none;
    cursor: pointer;
    font-size: 1rem;
    text-decoration: none;
  }

  .footer-links li button:hover,
  .footer-links li a:hover {
    color: white;
  }

  .footer-bottom {
    border-top: 1px solid #334155;
    margin-top: 3rem;
    padding-top: 2rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
  }

  .copyright {
    color: #94a3b8;
    text-align: center;
  }

  .legal-links {
    display: flex;
    gap: 1.5rem;
  }

  .legal-links a {
    color: #94a3b8;
    transition: color 0.3s ease;
    text-decoration: none;
  }

  .legal-links a:hover {
    color: white;
  }

  @media (min-width: 768px) {
    .footer {
      padding: 4rem 1rem;
    }

    .footer-grid {
      grid-template-columns: 2fr 1fr 1fr;
      gap: 2rem;
    }

    .footer-main {
      grid-column: span 1;
    }

    .footer-bottom {
      flex-direction: row;
      justify-content: space-between;
      align-items: center;
    }

    .copyright {
      text-align: left;
    }
  }

  @media (min-width: 1400px) {
    .container {
      max-width: 1600px;
    }
  }

  @media (min-width: 1920px) {
    .container {
      max-width: 1800px;
    }
  }

  @media (min-width: 2560px) {
    .container {
      max-width: 2000px;
    }
  }
</style> 