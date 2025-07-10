<script>
  import Header from './components/Header.svelte'
  import HeroPhoneSection from './components/HeroPhoneSection.svelte'
  import Features from './components/Features.svelte'
  import ControlSection from './components/ControlSection.svelte'
  import Pricing from './components/Pricing.svelte'
  import Testimonials from './components/Testimonials.svelte'
  import FAQ from './components/FAQ.svelte'
  import CTA from './components/CTA.svelte'
  import Footer from './components/Footer.svelte'

  
  // Estado global
  let currentSection = 'home'
  let isMenuOpen = false
  
  // Função para navegar suavemente
  function scrollToSection(sectionId) {
    const element = document.getElementById(sectionId)
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' })
      currentSection = sectionId
      isMenuOpen = false
    }
  }
  
  // Intersection Observer para animações
  import { onMount } from 'svelte'
  
  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('animate-in')
        }
      })
    }, { threshold: 0.1 })
    
    document.querySelectorAll('.animate-on-scroll').forEach(el => {
      observer.observe(el)
    })
  })
  
  // Scroll suave ao carregar com hash na URL
  onMount(() => {
    if (window.location.hash) {
      const sectionId = window.location.hash.replace('#', '');
      // Timeout para garantir que os componentes já renderizaram
      setTimeout(() => {
        scrollToSection(sectionId);
      }, 300);
    }
  });
  

</script>

<svelte:head>
  <title>Bot SMS Telegram - Envie e receba SMS pelo Telegram</title>
  <meta name="description" content="Bot para envio e recebimento de SMS via Telegram. Integração completa e fácil de usar.">
</svelte:head>

<Header {currentSection} {isMenuOpen} on:toggleMenu={() => isMenuOpen = !isMenuOpen} on:scrollTo={({ detail }) => scrollToSection(detail.sectionId)} />
<div class="scroll-content">
  <main>
  
    <HeroPhoneSection />
    <Features />
    <ControlSection />
    <FAQ />
    <Footer />
  </main>
</div>

<style>
  :global(*) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  :global(body) {
    font-family: 'Inter', sans-serif;
    line-height: 1.6;
    color: #fff;
    background: oklch(37.9% .146 265.522);
    overflow-x: hidden;
  }
  
  :global(html) {
    scroll-behavior: smooth;
    scroll-padding-top: 100px; /* Espaço para o header fixo */
  }
  
  :global(:root) {
    --primary-color: #0088cc;
    --secondary-color: #005580;
    --accent-color: #00bfff;
    --text-color: #333;
    --light-text: #666;
    --white: #ffffff;
    --light-bg: #f8f9fa;
    --border-color: #e9ecef;
    --shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    --shadow-lg: 0 10px 25px rgba(0, 0, 0, 0.15);
    --gradient: linear-gradient(135deg, #0088cc 0%, #00bfff 100%);
  }
  
  :global(.container) {
    max-width: 1400px;
    margin: 0 auto;
    padding: 0 20px;
    width: 100%;
  }
  
  :global(.animate-on-scroll) {
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.6s ease;
  }
  
  :global(.animate-on-scroll.animate-in) {
    opacity: 1;
    transform: translateY(0);
  }
  
  :global(.btn) {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    padding: 1rem 2rem;
    border-radius: 50px;
    text-decoration: none;
    font-weight: 600;
    transition: all 0.3s ease;
    border: none;
    cursor: pointer;
    font-size: 1rem;
  }
  
  :global(.btn-primary) {
    background: var(--white);
    color: var(--primary-color);
  }
  
  :global(.btn-primary:hover) {
    transform: translateY(-2px);
    box-shadow: var(--shadow-lg);
  }
  
  :global(.btn-secondary) {
    background: transparent;
    color: var(--white);
    border: 2px solid var(--white);
  }
  
  :global(.btn-secondary:hover) {
    background: var(--white);
    color: var(--primary-color);
  }
  
  :global(.section-header) {
    text-align: center;
    margin-bottom: 4rem;
  }
  
  :global(.section-title) {
    font-size: 2.5rem;
    font-weight: 700;
    margin-bottom: 1rem;
    color: var(--text-color);
  }
  
  :global(.section-subtitle) {
    font-size: 1.1rem;
    color: var(--light-text);
    max-width: 600px;
    margin: 0 auto;
  }
  
  main {
    width: 100%;
  }
  
  @media (max-width: 768px) {
    :global(.section-title) {
      font-size: 2rem;
    }
    
    :global(.container) {
      padding: 0 15px;
    }
    
    main {
      padding: 0;
    }
  }

  @media (min-width: 1400px) {
    :global(.container) {
      max-width: 1600px;
    }
  }

  @media (min-width: 1920px) {
    :global(.container) {
      max-width: 1800px;
    }
  }

  @media (min-width: 2560px) {
    :global(.container) {
      max-width: 2000px;
    }
  }
  
  /* Scrollbar personalizada */
  :global(::-webkit-scrollbar) {
    width: 7px;
    background: transparent;
  }
  
  :global(::-webkit-scrollbar-track) {
    background: #f1f1f1;
  }
  
  :global(::-webkit-scrollbar-thumb) {
    background: #888;
    border-radius: 8px;
    min-height: 40px;
    transition: background 0.2s;
  }
  
  :global(::-webkit-scrollbar-thumb:hover) {
    background: #555;
  }
  
  :global(::-webkit-scrollbar-corner) {
    background: transparent;
  }
  
  :global(html), :global(body), :global(#app) {
    height: 100%;
    width: 100%;
    position: relative;
  }
  
  main {
    display: block;
    width: 100%;
  }
  
  .scroll-content {
    width: 100%;
    min-height: 100vh;
  }
</style> 