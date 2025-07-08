<script>
  import { onMount } from 'svelte'
  import { fly, fade } from 'svelte/transition'

  let plans = [
    {
      name: 'Starter',
      price: '0',
      period: 'mês',
      description: 'Perfeito para começar',
      features: [
        'Até 100 assinantes',
        'Bot básico',
        'Pagamentos PIX',
        'Suporte por email',
        'Dashboard básico'
      ],
      popular: false,
      color: '#6b7280'
    },
    {
      name: 'Pro',
      price: '97',
      period: 'mês',
      description: 'Para criadores em crescimento',
      features: [
        'Até 1.000 assinantes',
        'Bot avançado',
        'Pagamentos PIX + Cartão',
        'Suporte prioritário',
        'Analytics completo',
        'Automações avançadas',
        'Integração com APIs'
      ],
      popular: true,
      color: '#0088cc'
    },
    {
      name: 'Enterprise',
      price: '297',
      period: 'mês',
      description: 'Para grandes comunidades',
      features: [
        'Assinantes ilimitados',
        'Bot personalizado',
        'Todos os métodos de pagamento',
        'Suporte 24/7',
        'Analytics avançado',
        'Automações ilimitadas',
        'API completa',
        'White label',
        'Consultoria incluída'
      ],
      popular: false,
      color: '#10b981'
    }
  ]

  let visiblePlans = []

  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          animatePlans()
        }
      })
    })

    const pricingSection = document.querySelector('.pricing')
    if (pricingSection) {
      observer.observe(pricingSection)
    }

    return () => observer.disconnect()
  })

  function animatePlans() {
    plans.forEach((plan, index) => {
      setTimeout(() => {
        visiblePlans = [...visiblePlans, plan]
      }, index * 200)
    })
  }

  function selectPlan(planName) {
    // Aqui você pode adicionar lógica para redirecionar para checkout
    console.log(`Plano selecionado: ${planName}`)
    alert(`Redirecionando para checkout do plano ${planName}`)
  }
</script>

<section class="pricing" id="pricing">
  <div class="container">
    <div class="section-header" in:fly={{ y: 50, duration: 800 }}>
      <h2>Planos e Preços</h2>
      <p>Escolha o plano ideal para sua comunidade. Sem taxas ocultas.</p>
    </div>

    <div class="pricing-grid">
      {#each plans as plan, index}
        {#if visiblePlans.includes(plan)}
          <div 
            class="pricing-card"
            class:popular={plan.popular}
            in:fly={{ y: 50, duration: 600, delay: index * 200 }}
            style="--accent-color: {plan.color}"
          >
            {#if plan.popular}
              <div class="popular-badge">Mais Popular</div>
            {/if}
            
            <div class="plan-header">
              <h3>{plan.name}</h3>
              <div class="price">
                <span class="currency">R$</span>
                <span class="amount">{plan.price}</span>
                <span class="period">/{plan.period}</span>
              </div>
              <p class="description">{plan.description}</p>
            </div>

            <div class="plan-features">
              <ul>
                {#each plan.features as feature}
                  <li>
                    <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                      <path d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    </svg>
                    {feature}
                  </li>
                {/each}
              </ul>
            </div>

            <button 
              class="plan-button"
              class:popular={plan.popular}
              on:click={() => selectPlan(plan.name)}
            >
              {plan.price === '0' ? 'Começar Grátis' : 'Escolher Plano'}
            </button>
          </div>
        {/if}
      {/each}
    </div>

  </div>
</section>

<style>
  .pricing {
    padding: 6rem 2rem;
    background: transparent;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
  }

  .section-header {
    text-align: center;
    margin-bottom: 4rem;
  }

  .section-header h2 {
    font-size: 3rem;
    font-weight: 700;
    color: #1f2937;
    margin-bottom: 1rem;
  }

  .section-header p {
    font-size: 1.25rem;
    color: #6b7280;
    max-width: 600px;
    margin: 0 auto;
  }

  .pricing-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 2rem;
    margin-bottom: 4rem;
  }

  .pricing-card {
    background: transparent;
    border-radius: 20px;
    padding: 2.5rem;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
    transition: all 0.3s ease;
    position: relative;
    border: 2px solid transparent;
  }

  .pricing-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
  }

  .pricing-card.popular {
    border-color: var(--accent-color);
    transform: scale(1.05);
  }

  .pricing-card.popular:hover {
    transform: scale(1.05) translateY(-8px);
  }

  .popular-badge {
    position: absolute;
    top: -12px;
    left: 50%;
    transform: translateX(-50%);
    background: var(--accent-color);
    color: white;
    padding: 0.5rem 1.5rem;
    border-radius: 20px;
    font-size: 0.875rem;
    font-weight: 600;
  }

  .plan-header {
    text-align: center;
    margin-bottom: 2rem;
  }

  .plan-header h3 {
    font-size: 1.5rem;
    font-weight: 700;
    color: #1f2937;
    margin-bottom: 1rem;
  }

  .price {
    display: flex;
    align-items: baseline;
    justify-content: center;
    gap: 0.25rem;
    margin-bottom: 1rem;
  }

  .currency {
    font-size: 1.25rem;
    font-weight: 600;
    color: #6b7280;
  }

  .amount {
    font-size: 3rem;
    font-weight: 900;
    color: var(--accent-color);
    line-height: 1;
  }

  .period {
    font-size: 1rem;
    color: #6b7280;
  }

  .description {
    color: #6b7280;
    font-size: 1rem;
  }

  .plan-features {
    margin-bottom: 2rem;
  }

  .plan-features ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .plan-features li {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    padding: 0.75rem 0;
    color: #374151;
    font-size: 1rem;
  }

  .plan-features li svg {
    color: var(--accent-color);
    flex-shrink: 0;
  }

  .plan-button {
    width: 100%;
    padding: 1rem 2rem;
    border: 2px solid var(--accent-color);
    border-radius: 12px;
    font-weight: 600;
    font-size: 1.1rem;
    cursor: pointer;
    transition: all 0.3s ease;
    background: transparent;
    color: var(--accent-color);
  }

  .plan-button:hover {
    background: var(--accent-color);
    color: white;
    transform: translateY(-2px);
  }

  .plan-button.popular {
    background: var(--accent-color);
    color: white;
  }

  .plan-button.popular:hover {
    background: var(--accent-color);
    color: white;
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(0, 136, 204, 0.4);
  }

  .pricing-cta {
    text-align: center;
    background: white;
    padding: 3rem;
    border-radius: 20px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  }

  .pricing-cta h3 {
    font-size: 2rem;
    font-weight: 700;
    color: #1f2937;
    margin-bottom: 1rem;
  }

  .pricing-cta p {
    color: #6b7280;
    font-size: 1.1rem;
    margin-bottom: 2rem;
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
  }

  .btn-outline:hover {
    background: #0088cc;
    color: white;
    transform: translateY(-2px);
  }

  @media (max-width: 768px) {
    .pricing {
      padding: 4rem 1rem;
    }

    .section-header h2 {
      font-size: 2.5rem;
    }

    .section-header p {
      font-size: 1.1rem;
    }

    .pricing-grid {
      grid-template-columns: 1fr;
      gap: 1.5rem;
    }

    .pricing-card {
      padding: 2rem;
    }

    .pricing-card.popular {
      transform: none;
    }

    .pricing-card.popular:hover {
      transform: translateY(-8px);
    }

    .amount {
      font-size: 2.5rem;
    }

    .pricing-cta {
      padding: 2rem;
    }

    .pricing-cta h3 {
      font-size: 1.75rem;
    }
  }
</style> 