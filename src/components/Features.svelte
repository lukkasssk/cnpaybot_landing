<script>
  import { onMount } from 'svelte'
  import { fly, scale, fade } from 'svelte/transition'
  import { elasticOut } from 'svelte/easing'
  import LordIcon from './LordIcon.svelte'
  
  let features = [
    {
      icon: 'hero-icon',
      heroIcon: 'cpu-chip',
      title: 'Sem programar',
      description: 'Configure seu bot sem precisar saber programação. Interface intuitiva e fácil de usar.',
      color: '#8b5cf6'
    },
    {
      icon: 'hero-icon',
      heroIcon: 'chart-bar',
      title: 'Taxa fixa',
      description: 'Apenas R$0,50 por transação aprovada. Sem surpresas ou taxas ocultas.',
      color: '#3b82f6'
    },
    {
      icon: 'hero-icon',
      heroIcon: 'device-phone-mobile',
      title: 'Personalização total',
      description: 'Customize mensagens, botões e toda a experiência do seu bot.',
      color: '#f59e0b'
    },
    {
      icon: 'hero-icon',
      heroIcon: 'bell',
      title: 'Suporte 24/7',
      description: 'Nossa equipe está sempre disponível para te ajudar quando precisar.',
      color: '#06b6d4'
    }
  ]
  
  let visibleFeatures = []
  let visibleMetrics = false
  
  // Dados das métricas
  let metrics = [
    { value: 0, target: 0.75, symbol: 'R$ ', label: 'Taxa por Venda', description: 'Apenas R$ 0,80 por cada venda que fizer' },
    { value: 0, target: 2, symbol: '', label: 'Recebimento', description: 'Pix em 2 dias úteis' },
    { value: 0, target: 99.9, symbol: '', label: 'Uptime', description: 'Sistema sempre online' }
  ]
  
  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          animateFeatures()
        }
      })
    })

    const featuresSection = document.querySelector('.features')
    if (featuresSection) {
      observer.observe(featuresSection)
    }
    
    // Observer para métricas
    const metricsObserver = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting && !visibleMetrics) {
          visibleMetrics = true
          animateMetrics()
        }
      })
    })

    const metricsSection = document.querySelector('.metrics-section')
    if (metricsSection) {
      metricsObserver.observe(metricsSection)
    }

    return () => {
      observer.disconnect()
      metricsObserver.disconnect()
    }
  })

  function animateFeatures() {
    features.forEach((feature, index) => {
      setTimeout(() => {
        visibleFeatures = [...visibleFeatures, feature]
      }, index * 200)
    })
  }
  
  function animateMetrics() {
    metrics.forEach((metric, index) => {
      const duration = 2000
      const steps = 60
      const increment = metric.target / steps
      let current = 0

      const timer = setInterval(() => {
        current += increment
        if (current >= metric.target) {
          current = metric.target
          clearInterval(timer)
        }
        
        // Tratamento específico para cada métrica
        if (index === 0) {
          // Taxa por Venda: 2 casas decimais
          metrics[index].value = parseFloat(current.toFixed(2))
        } else if (index === 2) {
          // Uptime: 1 casa decimal
          metrics[index].value = parseFloat(current.toFixed(1))
        } else {
          // Recebimento: número inteiro
          metrics[index].value = Math.floor(current)
        }
        
        metrics = [...metrics]
      }, duration / steps)
    })
  }
</script>

<section id="features" class="features">
  <div class="container">
    <div class="section-header" in:fly={{ y: 50, duration: 800 }}>
      <h2>Recursos Poderosos</h2>
      <p>Tudo que você precisa para monetizar sua comunidade no Telegram</p>
    </div>
    
    <div class="features-grid">
      {#each features as feature, index}
        {#if visibleFeatures.includes(feature)}
          <div 
            class="feature-card"
            in:fly={{ y: 50, duration: 600, delay: index * 100 }}
          >
            <div class="feature-icon">
              {#if feature.icon === 'hero-icon'}
                <svg class="hero-icon" width="32" height="32" fill="currentColor" viewBox="0 0 24 24">
                  {#if feature.heroIcon === 'credit-card'}
                    <path d="M4 5a3 3 0 013-3h10a3 3 0 013 3v14a3 3 0 01-3 3H7a3 3 0 01-3-3V5z"/>
                    <path d="M4 10h16"/>
                  {:else if feature.heroIcon === 'lock-closed'}
                    <path fill-rule="evenodd" d="M12 1.5a5.25 5.25 0 00-5.25 5.25v3a3 3 0 00-3 3v6.75a3 3 0 003 3h10.5a3 3 0 003-3v-6.75a3 3 0 00-3-3v-3c0-2.9-2.35-5.25-5.25-5.25zm3.75 8.25v-3a3.75 3.75 0 10-7.5 0v3h7.5z" clip-rule="evenodd"/>
                  {:else if feature.heroIcon === 'chart-bar'}
                    <path d="M18.375 2.25c-1.035 0-1.875.84-1.875 1.875v15.75c0 1.035.84 1.875 1.875 1.875h.75c1.035 0 1.875-.84 1.875-1.875V4.125c0-1.036-.84-1.875-1.875-1.875h-.75zM9.75 8.625c0-1.036.84-1.875 1.875-1.875h.75c1.036 0 1.875.84 1.875 1.875v11.25c0 1.035-.84 1.875-1.875 1.875h-.75a1.875 1.875 0 01-1.875-1.875V8.625zM3 13.125c0-1.036.84-1.875 1.875-1.875h.75c1.036 0 1.875.84 1.875 1.875v6.75c0 1.035-.84 1.875-1.875 1.875h-.75A1.875 1.875 0 013 19.875v-6.75z"/>
                  {:else if feature.heroIcon === 'cpu-chip'}
                    <path d="M14.25 7.756a.75.75 0 01.75-.75h2.25a.75.75 0 01.75.75v2.25a.75.75 0 01-.75.75H15a.75.75 0 01-.75-.75V7.756zM9.75 7.756a.75.75 0 01.75-.75h2.25a.75.75 0 01.75.75v2.25a.75.75 0 01-.75.75H10.5a.75.75 0 01-.75-.75V7.756zM3.75 7.756a.75.75 0 01.75-.75h2.25a.75.75 0 01.75.75v2.25a.75.75 0 01-.75.75H4.5a.75.75 0 01-.75-.75V7.756zM14.25 13.5a.75.75 0 01.75-.75h2.25a.75.75 0 01.75.75v2.25a.75.75 0 01-.75.75H15a.75.75 0 01-.75-.75V13.5zM9.75 13.5a.75.75 0 01.75-.75h2.25a.75.75 0 01.75.75v2.25a.75.75 0 01-.75.75H10.5a.75.75 0 01-.75-.75V13.5zM3.75 13.5a.75.75 0 01.75-.75h2.25a.75.75 0 01.75.75v2.25a.75.75 0 01-.75.75H4.5a.75.75 0 01-.75-.75V13.5z"/>
                  {:else if feature.heroIcon === 'device-phone-mobile'}
                    <path d="M10.5 1.875a1.125 1.125 0 012.25 0v8.219c.75.311 1.29.938 1.29 1.656 0 .828-.54 1.345-1.29 1.656V18.75a1.125 1.125 0 01-2.25 0v-5.594c-.75-.311-1.29-.828-1.29-1.656 0-.718.54-1.345 1.29-1.656V1.875z"/>
                  {:else if feature.heroIcon === 'megaphone'}
                    <path d="M13.5 4.06c0-1.336-1.616-2.005-2.56-1.06l-4.5 4.5H4.508c-1.141 0-2.318.664-2.66 1.905A9.76 9.76 0 001.5 12c0 .898.121 1.768.35 2.595.341 1.24 1.518 1.905 2.659 1.905h1.93l4.5 4.5c.945.945 2.561.276 2.561-1.06V4.06zM17.78 9.22a.75.75 0 10-1.06-1.06l-.97.97-.97-.97a.75.75 0 00-1.06 1.06l1.5 1.5a.75.75 0 001.06 0l1.5-1.5z"/>
                  {:else if feature.heroIcon === 'bell'}
                    <path d="M14.857 17.082a23.848 23.848 0 005.454-1.31A8.967 8.967 0 0118 9.75v-.7V9A6 6 0 006 9v.75a8.967 8.967 0 01-2.312 6.022c1.733.64 3.56 1.085 5.455 1.31m5.714 0a24.255 24.255 0 01-5.714 0m5.714 0a3 3 0 11-5.714 0"/>
                  {:else if feature.heroIcon === 'document-chart-bar'}
                    <path fill-rule="evenodd" d="M5.625 1.5c-1.036 0-1.875.84-1.875 1.875v17.25c0 1.035.84 1.875 1.875 1.875h12.75c1.035 0 1.875-.84 1.875-1.875V12.75A3.75 3.75 0 0016.5 9h-1.875a1.875 1.875 0 01-1.875-1.875V5.25A3.75 3.75 0 009 1.5H5.625zM7.5 15a.75.75 0 01.75-.75h7.5a.75.75 0 010 1.5h-7.5A.75.75 0 017.5 15zm.75 2.25a.75.75 0 000 1.5H12a.75.75 0 000-1.5H8.25z" clip-rule="evenodd"/>
                    <path d="M12.971 1.816A5.23 5.23 0 0114.25 5.25v1.875c0 .207.168.375.375.375H16.5A5.23 5.23 0 0118 7.971v8.278a1.875 1.875 0 01-1.875 1.875H5.625A1.875 1.875 0 013.75 16.5V7.971c0-.432.111-.857.32-1.243.375-.207.744-.332 1.18-.332H12a.75.75 0 00.75-.75V5.25a.75.75 0 00-.779-.434z"/>
                  {:else if feature.heroIcon === 'globe-alt'}
                    <path fill-rule="evenodd" d="M12 2.25c-5.385 0-9.75 4.365-9.75 9.75s4.365 9.75 9.75 9.75 9.75-4.365 9.75-9.75S17.385 2.25 12 2.25zM8.547 4.505a8.273 8.273 0 011.05-.634 5.987 5.987 0 00-.884 1.58 6.62 6.62 0 00-1.618 1.756l-.25-.433c.271-.527.542-1.035.802-1.269zM12 20.25a8.287 8.287 0 01-1.449-.148 9.687 9.687 0 01-1.663-.116 8.351 8.351 0 01-1.246-.213 6.135 6.135 0 01-1.653-.119c-2.793-.526-5.022-2.329-5.022-4.68 0-.528 2.642 1.96 6.48 3.348 3.878 1.388 9.297 2.108 9.297 2.108s-5.418-.72-9.297-2.108c-3.838-1.388-6.48-1.876-6.48-3.348 0-2.351 2.229-4.154 5.022-4.68.528-.1 1.092-.181 1.653-.119.409-.078.836-.12 1.246-.213.591-.124 1.189-.29 1.821-.442a.75.75 0 00.291-1.451 9.952 9.952 0 001.51.255A8.023 8.023 0 0012 3.75c-.682 0-1.349.097-1.988.28A6.423 6.423 0 0112 5.25c.682 0 1.349.097 1.988.28.64.183 1.23.442 1.786.766a.75.75 0 001.451-.291 11.5 11.5 0 00-6.48-3.348C9.642 1.96 12.642.432 12.642 0c0 .528-2.642 1.96-6.48 3.348S0 6.228 0 6.756c0 2.351 2.229 4.154 5.022 4.68.528.1 1.092.181 1.653.119.409-.078.836-.12 1.246-.213.591-.124 1.189-.29 1.821-.442a.75.75 0 00.291-1.451 9.952 9.952 0 001.51.255A8.023 8.023 0 0012 20.25z" clip-rule="evenodd"/>
                  {/if}
                </svg>
              {:else}
                <span>{feature.icon}</span>
              {/if}
            </div>
            <h3>{feature.title}</h3>
            <p>{feature.description}</p>
          </div>
        {/if}
      {/each}
    </div>
    

    
    <!-- Seção de Métricas -->
    <div class="metrics-section" id="pricing">
      <div class="section-header" in:fly={{ y: 50, duration: 800 }}>
        <h2>Métricas Impressionantes</h2>
        <p>Números que comprovam nossa excelência</p>
      </div>
      
      <div class="metrics-container">
        <div class="metrics-grid">
          {#each metrics as metric, index}
            <div class="metric-card" in:fly={{ y: 50, duration: 600, delay: 200 + (index * 200) }}>
              <div class="metric-icon">
                <lord-icon 
                  src={index === 0 ? "https://cdn.lordicon.com/avwubsdy.json" : 
                       index === 1 ? "https://cdn.lordicon.com/inmhgmpp.json" : 
                       index === 2 ? "https://cdn.lordicon.com/qhgmphtg.json" :
                       "https://cdn.lordicon.com/avwubsdy.json"}
                  trigger="loop" 
                  delay={2000 + (index * 500)} 
                  colors="primary:#3B82F6,secondary:#93C5FD" 
                  style="width: 48px; height: 48px;"
                ></lord-icon>
              </div>
              <div class="metric-content">
                <div class="metric-value">
                  {index === 1 ? 'D+' : ''}{index === 2 ? '' : metric.symbol}{index === 0 ? metric.value.toFixed(2) : index === 2 ? metric.value.toFixed(1) : Math.floor(metric.value)}{index === 2 ? '%' : ''}
                </div>
                <div class="metric-label">{metric.label}</div>
                <div class="metric-description">{metric.description}</div>
              </div>
            </div>
          {/each}
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .features {
    padding: 6rem 2rem;
    background: transparent;
  }
  
  .container {
    max-width: 1400px;
    margin: 0 auto;
    width: 100%;
  }
  
  .section-header {
    text-align: center;
    margin-bottom: 4rem;
  }
  
  .section-header h2 {
    font-size: 3rem;
    font-weight: 700;
    color:rgb(255, 255, 255);
    margin-bottom: 1rem;
  }
  
  .section-header p {
    font-size: 1.25rem;
    color: #fbfbfb;
    max-width: 600px;
    margin: 0 auto;
  }
  
  .features-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 2rem;
    margin-bottom: 4rem;
  }
  
  .feature-card {
    background: rgba(30, 41, 59, 0.8);
    padding: 1.5rem;
    border-radius: 12px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
    border: 1px solid rgba(51, 65, 85, 0.7);
  }
  
  .feature-card::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, rgba(255, 255, 255, 0.05) 0%, rgba(255, 255, 255, 0.02) 100%);
    opacity: 0;
    transition: opacity 0.3s ease;
  }
  
  .feature-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
    border-color: rgba(51, 65, 85, 0.9);
  }
  
  .feature-card:hover::after {
    opacity: 1;
  }
  
  .feature-icon {
    width: 80px;
    height: 80px;
    border-radius: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 1.5rem;
    font-size: 2rem;
    color: white;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }
  
  .feature-icon::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    opacity: 0;
    transition: opacity 0.3s ease;
  }
  
  .feature-card:hover .feature-icon {
    transform: scale(1.1);
  }
  
  .feature-card:hover .feature-icon::before {
    opacity: 1;
  }
  
  .feature-icon :global(lord-icon) {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .hero-icon {
    width: 32px;
    height: 32px;
    color: white;
    transition: transform 0.3s ease;
  }
  
  .feature-card:hover .hero-icon {
    transform: scale(1.1);
  }
  

  
  /* Estilos da Seção de Métricas */
  .metrics-section {
    margin-top: 6rem;
    padding: 4rem 0;
  }
  
  .metrics-container {
    max-width: 1200px;
    margin: 0 auto;
  }
  
  .metrics-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    margin-top: 3rem;
  }
  
  .metric-card {
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 20px;
    padding: 2rem;
    text-align: center;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }
  
  .metric-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 4px;
    background: linear-gradient(90deg, #3B82F6, #93C5FD);
  }
  
  .metric-card:hover {
    transform: translateY(-8px);
    box-shadow: rgba(0, 0, 0, 0.3) 0px 10px 30px 0px, 
                rgba(255, 255, 255, 0.05) 0px 0px 0px 1px, 
                rgba(255, 255, 255, 0.1) 0px 1px 0px 0px inset;
  }
  
  .metric-icon {
    display: flex;
    justify-content: center;
    margin-bottom: 1.5rem;
  }
  
  .metric-content {
    color: #ffffff;
  }
  
  .metric-value {
    font-size: 2.5rem;
    font-weight: 700;
    color: #ffffff;
    margin-bottom: 0.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.25rem;
  }
  
  .metric-symbol {
    font-size: 1.5rem;
    font-weight: 600;
    color: #93C5FD;
  }
  
  .metric-label {
    font-size: 1.25rem;
    font-weight: 600;
    color: #ffffff;
    margin-bottom: 0.5rem;
  }
  
  .metric-description {
    font-size: 1rem;
    color: #9ca3af;
    line-height: 1.5;
  }
  
  @media (max-width: 768px) {
    .metrics-grid {
      grid-template-columns: 1fr;
      gap: 1.5rem;
    }
    
    .metric-card {
      padding: 1.5rem;
    }
    
    .metric-value {
      font-size: 2rem;
    }
    
    .metric-label {
      font-size: 1.1rem;
    }
  }
  
  .feature-card h3 {
    font-size: 1.125rem;
    font-weight: 600;
    color: white;
    margin-bottom: 0.5rem;
  }
  
  .feature-card p {
    color: #94a3b8;
    line-height: 1.6;
    font-size: 1rem;
  }
  
  .features-cta {
    text-align: center;
    background: white;
    padding: 3rem;
    border-radius: 20px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  }
  
  .features-cta h3 {
    font-size: 2rem;
    font-weight: 700;
    color: #1f2937;
    margin-bottom: 1rem;
  }
  
  .features-cta p {
    color: #fbfbfb;
    font-size: 1.1rem;
    margin-bottom: 2rem;
  }
  
  .btn-primary {
    background: linear-gradient(135deg, #0088cc, #00a8ff);
    color: white;
    border: none;
    padding: 1rem 2.5rem;
    border-radius: 12px;
    font-weight: 600;
    font-size: 1.1rem;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 15px rgba(0, 136, 204, 0.3);
  }
  
  .btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(0, 136, 204, 0.4);
  }
  
  @media (max-width: 768px) {
    .features {
      padding: 4rem 1rem;
    }
    
    .section-header h2 {
      font-size: 2.5rem;
    }
    
    .section-header p {
      font-size: 1.1rem;
    }
    
    .features-grid {
      grid-template-columns: 1fr;
      gap: 1.5rem;
    }
    
    .feature-card {
      padding: 1.5rem;
    }
    
    .feature-icon {
      width: 60px;
      height: 60px;
      font-size: 1.5rem;
    }
    
    .feature-card h3 {
      font-size: 1.125rem;
    }
    
    .features-cta {
      padding: 2rem;
    }
    
    .features-cta h3 {
      font-size: 1.75rem;
    }
  }
</style> 