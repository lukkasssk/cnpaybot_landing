<script>
  import { onMount } from 'svelte';
  import { fade } from 'svelte/transition';
  import { createEventDispatcher } from 'svelte';
  
  // Props do componente
  export let currentSection = 'home';
  export let isMenuOpen = false;
  
  const dispatch = createEventDispatcher();
  
  let scrolled = false;
  let scrollOpacity = 0;
  let isScrollingDown = false;
  let lastScrollY = 0;
  let scrollDirection = 'up';
  let hasScrolled = false;

  onMount(() => {
    // Inicializa lastScrollY com a posição atual
    lastScrollY = window.scrollY;
    
    const handleScroll = () => {
      const scrollY = window.scrollY;
      const newScrolled = scrollY > 50;
      
      // Marca que já houve scroll
      if (scrollY > 0) {
        hasScrolled = true;
      }
      
      // Detecta a direção do scroll
      if (scrollY > lastScrollY) {
        scrollDirection = 'down';
        isScrollingDown = scrollY > 100; // Só ativa após 100px
      } else if (scrollY < lastScrollY) {
        scrollDirection = 'up';
        isScrollingDown = false;
      }
      
      lastScrollY = scrollY;
      
      // Debug para verificar se está funcionando
      console.log('Scroll Y:', scrollY, 'Scrolled:', newScrolled, 'Direction:', scrollDirection, 'Scrolling Down:', isScrollingDown);
      
      // Log mais visível quando a classe é aplicada
      if (newScrolled && !scrolled) {
        console.log('🎯 CLASSE .scrolled APLICADA!');
      } else if (!newScrolled && scrolled) {
        console.log('❌ CLASSE .scrolled REMOVIDA!');
      }
      
      // Só executa os logs de scroll se já houve scroll anterior
      if (hasScrolled) {
        if (isScrollingDown && scrollY > 100) {
          console.log('⬇️ SCROLLING DOWN - Box shadow branco ativo!');
        } else if (!isScrollingDown && scrollDirection === 'up') {
          console.log('⬆️ SCROLLING UP - Box shadow branco removido!');
        }
      }
      
      scrolled = newScrolled;
      
      // Calcula a opacidade baseada no scroll (0 a 0.8)
      if (scrollY > 0) {
        scrollOpacity = Math.min(scrollY / 200, 0.8); // Máximo 0.8 de opacidade
      } else {
        scrollOpacity = 0;
      }
    };
    
    // Executa uma vez no início para verificar o estado inicial
    handleScroll();
    
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  });

  function toggleMobileMenu() {
    // Dispatch event para o componente pai
    dispatch('toggleMenu');
  }

  function scrollToSection(sectionId) {
    const element = document.getElementById(sectionId);
    if (element) {
      // Fecha o menu mobile se estiver aberto
      if (isMenuOpen) {
        dispatch('toggleMenu');
      }

      // Calcula a altura real do header fixo
      const header = document.querySelector('header');
      const headerHeight = header ? header.offsetHeight + 20 : 100; // 20px extra para margem
      const elementRect = element.getBoundingClientRect();
      const absoluteElementTop = elementRect.top + window.pageYOffset;
      const targetPosition = absoluteElementTop - headerHeight;
      const startPosition = window.pageYOffset;
      const distance = targetPosition - startPosition;
      const duration = 900; // Duração da animação em ms
      let start = null;

      // Função de easing (easeInOutCubic)
      function easeInOutCubic(t) {
        return t < 0.5 ? 4 * t * t * t : (t - 1) * (2 * t - 2) * (2 * t - 2) + 1;
      }

      function animation(currentTime) {
        if (start === null) start = currentTime;
        const timeElapsed = currentTime - start;
        const progress = Math.min(timeElapsed / duration, 1);
        const easedProgress = easeInOutCubic(progress);
        window.scrollTo(0, startPosition + distance * easedProgress);
        if (timeElapsed < duration) {
          requestAnimationFrame(animation);
        }
      }
      requestAnimationFrame(animation);
    }
    dispatch('scrollTo', { sectionId });
  }
</script>

<header class:scrolled class:scrolling-down={isScrollingDown} style="--scroll-opacity: {scrollOpacity}">
  <!-- Indicador visual temporário -->
  {#if scrolled}
    <div style="position: absolute; top: 5px; right: 5px; background: red; color: white; padding: 2px 6px; font-size: 10px; border-radius: 3px; z-index: 1001;">
      SCROLLED
    </div>
  {/if}
  
  {#if isScrollingDown}
    <div style="position: absolute; top: 5px; right: 80px; background: blue; color: white; padding: 2px 6px; font-size: 10px; border-radius: 3px; z-index: 1001;">
      DOWN
    </div>
  {/if}
  
  <nav>
    <div class="nav-container">
      <div class="logo">
        <img src="../../static/imagem/cnbot_logo.png" alt="CN Bot Logo" style="height:40px; width:auto; display:block;" />
      </div>

      <div class="nav-links" class:open={isMenuOpen}>
        <button class="mobile-close-btn" on:click={toggleMobileMenu}>
          <svg width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M18 6L6 18M6 6l12 12"/>
          </svg>
        </button>
        <a href="#hero" on:click={() => scrollToSection('hero')}>Início</a>
        <a href="#features" on:click={() => scrollToSection('features')}>Recursos</a>
        <a href="#how-it-works" on:click={() => scrollToSection('how-it-works')}>Como Funciona</a>
        <a href="#pricing" on:click={() => scrollToSection('pricing')}>Preços</a>
        <a href="#faq" on:click={() => scrollToSection('faq')}>FAQ</a>
        <a href="#suporte" on:click={() => scrollToSection('suporte')}>Contato</a>
      </div>

      <div class="nav-buttons">
        <button class="btn-secondary s-c1MG4BWNDc59" on:click={() => window.open('https://t.me/cnpayy_bot', '_blank')}>Falar Com Gerente</button>
        <button class="mobile-menu-btn" class:open={isMenuOpen} on:click={toggleMobileMenu}>
          {#if isMenuOpen}
            <!-- Ícone X quando menu aberto -->
            <svg width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M18 6L6 18M6 6l12 12"/>
            </svg>
          {:else}
            <!-- Ícone hambúrguer quando menu fechado -->
            <svg width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M3 12h18M3 6h18M3 18h18"/>
            </svg>
          {/if}
        </button>
      </div>
    </div>
  </nav>
</header>

<style>
  header {
    position: relative;
    left: 0;
    right: 0;
    width: 100%;
    justify-self: center;
    z-index: 1000;
    background: white;
    backdrop-filter: blur(10px);
    transition: all 0.3s ease;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, calc(var(--scroll-opacity) * 0.1));
  }

  header.scrolled {
    border-bottom: 3px solid #0088cc;
    box-shadow: 0 4px 15px -5px rgba(0, 0, 0, 0.3);
    background: white;
    transform: translateY(0);
  }

  header.scrolling-down {
    box-shadow: 0 8px 25px -5px rgba(255, 255, 255, 0.9), 0 4px 6px -1px rgba(0, 0, 0, calc(var(--scroll-opacity) * 0.1));
    border-bottom: 3px solid rgba(255, 255, 255, 0.5);
  }

  nav {
    padding: 1rem 0;
    width: 100%;
  }

  .nav-container {
    max-width: 1400px;
    width: 100%;
    margin: 0 auto;
    display: flex;
    gap: 1rem; 
    align-items: center;
    justify-content: space-between;
    padding: 0 32px;
    height: 64px;
    background: rgba(0, 0, 0, 0);
    border-radius: 18px;
    box-shadow: 0 2px 12px rgba(0,0,0,0.04);
  }

  .logo {
    display: flex;
    align-items: center;
    gap: 10px;
    font-weight: 700;
    font-size: 1.25rem;
    color: #0088cc;
  }

  .nav-links {
    display: flex;
    gap: 32px;
    flex: 1;
    justify-content: center;
    align-items: center;
  }

  .nav-links a {
    text-decoration: none;
    color: oklch(55.6% 0 0);
    font-weight: 500;
    font-size: 14px;
    line-height: 14px;
    transition: color 0.3s ease;
    position: relative;
  }

  .nav-links a:hover {
    color: #0088cc;
  }

  .nav-links a::after {
    content: '';
    position: absolute;
    bottom: -4px;
    left: 0;
    width: 0;
    height: 2px;
    background: #0088cc;
    transition: width 0.3s ease;
  }

  .nav-links a:hover::after {
    width: 100%;
  }

  .nav-buttons {
    display: flex;
    align-items: center;
    gap: 16px;
  }

  .btn-secondary {
    border: 2px solid #0088cc;
    background: oklch(60% .2 250);
    color: #ffffff;
    border-radius: 5px;
    padding: 8px 22px;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.2s, color 0.2s;
  }

  .mobile-menu-btn {
    display: none;
    background: none;
    border: none;
    cursor: pointer;
    padding: 0.5rem;
    color: oklch(55.6% 0 0);
    transition: color 0.3s ease;
  }

  .mobile-close-btn {
    display: none;
    position: absolute;
    top: 1rem;
    right: 1rem;
    background: none;
    border: none;
    cursor: pointer;
    padding: 0.5rem;
    color: oklch(55.6% 0 0);
    transition: color 0.3s ease;
  }

  .mobile-close-btn:hover {
    color: #0088cc;
  }

  .mobile-menu-btn:hover {
    color: #0088cc;
  }

  .mobile-menu-btn svg {
    width: 24px;
    height: 24px;
    transition: all 0.3s ease;
  }

  @media (max-width: 768px) {
    nav {
      padding: 1rem;
    }

    .nav-links {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      background: #0b0b0b;
      flex-direction: column;
      padding: 2rem;
      gap: 1.5rem;
      transform: translateY(-100%);
      opacity: 0;
      visibility: hidden;
      transition: all 0.3s ease;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
      justify-content: flex-start;
      align-items: center;
      z-index: 9999;
      padding-top: 6rem;
      min-height: 300px;
      border-bottom-left-radius: 20px;
      border-bottom-right-radius: 20px;
    }

    .nav-links a {
      color: oklch(55.6% 0 0);
      font-size: 1.2rem;
      font-weight: 600;
      padding: 0.75rem 0;
    }

    .nav-links a:hover {
      color: #0088cc;
    }

    .nav-links.open {
      transform: translateY(0);
      opacity: 1;
      visibility: visible;
    }

    .mobile-menu-btn {
      display: flex;
    }

    .mobile-menu-btn svg {
      width: 24px;
      height: 24px;
      transition: all 0.3s ease;
    }

    .mobile-close-btn {
      display: block;
    }
  }

  @media (max-width: 900px) {
    .nav-container {
      padding: 0 12px;
    }
    .nav-links {
      gap: 16px;
    }
    .nav-buttons {
      gap: 8px;
    }
  }

  @media (min-width: 1400px) {
    .nav-container {
      max-width: 1600px;
    }
  }

  @media (min-width: 1920px) {
    .nav-container {
      max-width: 1800px;
    }
  }

  @media (min-width: 2560px) {
    .nav-container {
      max-width: 2000px;
    }
  }
</style> 