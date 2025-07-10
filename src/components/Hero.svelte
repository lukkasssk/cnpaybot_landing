<script>
  import { onMount } from 'svelte'
  import { fade, fly, scale } from 'svelte/transition'
  import { elasticOut, bounceOut } from 'svelte/easing'
  import LordIcon from './LordIcon.svelte'
  
  let showContent = false
  let showStats = false
  let showBot = false
  
  onMount(() => {
    setTimeout(() => showContent = true, 100)
    setTimeout(() => showStats = true, 800)
    setTimeout(() => showBot = true, 1200)
  })
  
  // Stats counter animation
  let stats = [
    { number: 0, target: 5000, label: 'Criadores Ativos', suffix: '+' },
    { number: 0, target: 50000, label: 'Assinantes', suffix: '+' },
    { number: 0, target: 1000000, label: 'Receita Gerada', suffix: 'R$' }
  ]
  
  let animated = false
  
  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting && !animated) {
          animateStats()
          animated = true
        }
      })
    })

    const heroSection = document.querySelector('.hero')
    if (heroSection) {
      observer.observe(heroSection)
    }

    return () => observer.disconnect()
  })
  
  function animateStats() {
    stats.forEach((stat, index) => {
      const duration = 2000
      const steps = 60
      const increment = stat.target / steps
      let current = 0

      const timer = setInterval(() => {
        current += increment
        if (current >= stat.target) {
          current = stat.target
          clearInterval(timer)
        }
        stats[index].number = Math.floor(current)
        stats = [...stats]
      }, duration / steps)
    })
  }
  
  function scrollToPricing() {
    const element = document.getElementById('pricing')
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' })
    }
  }


</script>

<section class="hero" id="hero">
  <div class="hero-container">
    <div class="hero-content hero-single" in:fly={{ y: 50, duration: 800, delay: 200 }}>
      <h1 class="main-title">
        Rapidez e segurança para você <span class="highlight-gradient">lucrar mais.</span>
      </h1>
      <p class="hero-description">
        Uma plataforma para você vender a assinatura da sua Comunidade VIP ou conteúdo individual no Telegram.
      </p>
      <div class="hero-buttons">
        <button class="btn-primary">
          CRIAR MEU BOT
        </button>
      </div>
    </div>

  </div>

</section>

<style>
  .hero {
    display: flex;
    align-items: center;
    position: relative;
    overflow: hidden;
    padding: 0 2rem 4rem;
  }

  .hero-container {
    max-width: 600px;
    margin: 0 auto;
    width: 100%;
  }

  .hero-content {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: center;
    margin-bottom: 4rem;
    max-width: 800px;
  }

  .hero-text h1 {
    font-size: 3.0rem;
    font-weight: 700;
    line-height: 1.2;
    margin-bottom: 1.5rem;
    color: #1f2937;
    text-align: left;
  }

  .highlight-gradient {
    background: linear-gradient(90deg, #00c6fb 0%, #005bea 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    color: transparent;
    font-weight: 800;
  }

  .hero-description {
    font-size: 1.25rem;
    color: #fbfbfb;
    margin-bottom: 2.5rem;
    line-height: 1.6;
    text-align: left;
    max-width: 600px;
    word-wrap: break-word;
  }

  .hero-buttons {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    justify-content: flex-start;
  }

  .btn-primary {
    background: linear-gradient(135deg, #0088cc, #00a8ff);
    color: white;
    border: none;
    padding: 1.5rem 3rem;
    border-radius: 16px;
    font-weight: 700;
    font-size: 1.3rem;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 8px 30px rgba(0, 136, 204, 0.4), 0 4px 15px rgba(0, 0, 0, 0.1);
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .btn-primary:hover {
    transform: translateY(-3px);
    box-shadow: 0 12px 40px rgba(0, 136, 204, 0.5), 0 8px 25px rgba(0, 0, 0, 0.15);
  }

  .btn-outline {
    background: transparent;
    color: #0088cc;
    border: 2px solid #0088cc;
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
    background: #0088cc;
    color: white;
    transform: translateY(-2px);
  }

  .telegram-mockup {
    background: white;
    border-radius: 20px;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
    overflow: hidden;
    max-width: 400px;
    margin: 0 auto;
  }

  .mockup-header {
    background: #0088cc;
    color: white;
    padding: 1rem;
    display: flex;
    align-items: center;
    gap: 1rem;
  }

  .mockup-dots {
    display: flex;
    gap: 4px;
  }

  .mockup-dots span {
    width: 8px;
    height: 8px;
    background: rgba(255, 255, 255, 0.7);
    border-radius: 50%;
  }

  .mockup-title {
    font-weight: 600;
  }

  .mockup-content {
    padding: 1rem;
    background: #f8fafc;
  }

  .message {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 1rem;
  }

  .message-avatar {
    width: 32px;
    height: 32px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #0088cc;
    color: white;
    font-size: 1.2rem;
  }

  .message-content {
    flex: 1;
  }

  .message-text {
    background: white;
    padding: 0.75rem 1rem;
    border-radius: 12px;
    margin-bottom: 0.25rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  .user-message .message-text {
    background: #0088cc;
    color: white;
  }

  .message-buttons {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin-top: 0.5rem;
  }

  .plan-btn {
    background: #10b981;
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 8px;
    font-size: 0.9rem;
    cursor: pointer;
    transition: all 0.3s ease;
  }

  .plan-btn:hover {
    background: #059669;
  }

  .message-time {
    font-size: 0.75rem;
    color: #9ca3af;
    text-align: right;
  }

  .hero-stats {
    text-align: center;
  }

  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 2rem;
    max-width: 800px;
    margin: 0 auto;
  }

  .stat-item {
    padding: 2rem;
    background: white;
    border-radius: 16px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
    transition: transform 0.3s ease;
  }

  .stat-item:hover {
    transform: translateY(-4px);
  }

  .stat-number {
    font-size: 2.5rem;
    font-weight: 700;
    color: #0088cc;
    margin-bottom: 0.5rem;
  }

  .stat-label {
    color: #fbfbfb;
    font-weight: 500;
  }

  .hero-background {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: -1;
    overflow: hidden;
  }

  .bg-shape {
    position: absolute;
    border-radius: 50%;
    background: linear-gradient(135deg, rgba(0, 136, 204, 0.1), rgba(0, 168, 255, 0.1));
  }

  .bg-shape-1 {
    width: 300px;
    height: 300px;
    top: -150px;
    right: -150px;
  }

  .bg-shape-2 {
    width: 200px;
    height: 200px;
    bottom: -100px;
    left: -100px;
  }

  .bg-shape-3 {
    width: 150px;
    height: 150px;
    top: 50%;
    right: 10%;
  }

  .hero-extra {
    margin-top: 2.5rem;
    text-align: center;
    background: rgba(20,20,20,0.7);
    border-radius: 18px;
    padding: 2rem 1.5rem;
    box-shadow: 0 2px 12px rgba(0,0,0,0.08);
    color: #fff;
    max-width: 420px;
    margin-left: auto;
    margin-right: auto;
  }
  .hero-extra h2 {
    font-size: 1.5rem;
    font-weight: 700;
    margin-bottom: 0.7rem;
  }
  .hero-extra p {
    font-size: 1.1rem;
    margin-bottom: 1.2rem;
    color: #d1d5db;
  }
  .btn-specialist {
    background: linear-gradient(135deg, #0088cc, #00a8ff);
    color: #fff;
    border: none;
    border-radius: 24px;
    padding: 0.8rem 2rem;
    font-weight: 600;
    font-size: 1rem;
    cursor: pointer;
    transition: background 0.2s;
  }
  .hero-content.hero-single {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: center;
    text-align: left;
    gap: 1.5rem;
    margin-bottom: 4rem;
  }
  .hero-content.hero-single .main-title {
    font-size: 3.5rem;
    font-weight: 700;
    line-height: 1.1;
    margin-bottom: 1.5rem;
    color: rgb(255, 255, 255);
    max-width: 800px;
    text-align: left;
  }
  .hero-content.hero-single .hero-description {
    font-size: 1.25rem;
    color: #fbfbfb;
    margin-bottom: 2.5rem;
    line-height: 1.6;
  }
  .hero-content.hero-single .hero-buttons {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    justify-content: flex-start;
  }

  @media (max-width: 768px) {
    .hero {
      padding: 0px 1rem 2rem;
    }

    .hero-content {
      grid-template-columns: 1fr;
      gap: 2rem;
      text-align: center;
    }

    .hero-text h1 {
      font-size: 2.5rem;
    }

    .hero-content.hero-single .main-title {
      font-size: 2.5rem;
      line-height: 1.1;
      margin-bottom: 1rem;
      text-align: left;
    }

    .hero-description {
      font-size: 1.1rem;
      text-align: left;
      max-width: 100%;
    }

    .hero-content.hero-single .hero-description {
      font-size: 1rem;
      margin-bottom: 2rem;
      text-align: left;
      max-width: 100%;
    }

    .hero-buttons {
      justify-content: center;
    }

    .btn-primary {
      padding: 1.2rem 2.5rem;
      font-size: 1.1rem;
    }

    .stats-grid {
      grid-template-columns: 1fr;
      gap: 1rem;
    }

    .stat-item {
      padding: 1.5rem;
    }

    .stat-number {
      font-size: 2rem;
    }
  }

  @media (max-width: 480px) {
    .hero-content.hero-single .main-title {
      font-size: 2rem;
      line-height: 1.1;
    }

    .hero-content.hero-single .hero-description {
      font-size: 0.95rem;
    }

    .btn-primary {
      padding: 1rem 2rem;
      font-size: 1rem;
    }
  }


</style> 