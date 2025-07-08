<script>
  import { onMount } from 'svelte';
  import { fly, fade } from 'svelte/transition';

  let testimonials = [
    {
      name: 'Ana Silva',
      role: 'Criadora de Conteúdo',
      avatar: '👩‍💻',
      content: 'Consegui monetizar minha comunidade de 5.000 pessoas em apenas 2 meses. A plataforma é incrível!',
      rating: 5,
      revenue: 'R$ 15.000/mês'
    },
    {
      name: 'Carlos Santos',
      role: 'Influencer Tech',
      avatar: '👨‍💼',
      content: 'O bot automatizou 90% do meu processo de vendas. Agora posso focar no conteúdo.',
      rating: 5,
      revenue: 'R$ 25.000/mês'
    },
    {
      name: 'Mariana Costa',
      role: 'Coach de Negócios',
      avatar: '👩‍🎓',
      content: 'Transformei meu grupo de coaching em uma fonte de renda consistente. Recomendo para todos!',
      rating: 5,
      revenue: 'R$ 8.500/mês'
    },
    {
      name: 'Roberto Lima',
      role: 'Especialista em Marketing',
      avatar: '👨‍💻',
      content: 'A integração com PIX e cartão facilitou muito. Meus clientes adoram a facilidade de pagamento.',
      rating: 5,
      revenue: 'R$ 12.000/mês'
    },
    {
      name: 'Fernanda Alves',
      role: 'Consultora Financeira',
      avatar: '👩‍💼',
      content: 'O analytics me ajuda a entender exatamente o que está funcionando. ROI incrível!',
      rating: 5,
      revenue: 'R$ 18.000/mês'
    },
    {
      name: 'Lucas Mendes',
      role: 'Criador de Cursos',
      avatar: '👨‍🎓',
      content: 'Automatizei todo o processo de vendas. Agora vendo 24/7 sem precisar estar online.',
      rating: 5,
      revenue: 'R$ 30.000/mês'
    }
  ];

  let visibleTestimonials = [];
  let currentSlide = 0;

  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          animateTestimonials();
        }
      });
    });

    const testimonialsSection = document.querySelector('.testimonials');
    if (testimonialsSection) {
      observer.observe(testimonialsSection);
    }

    return () => observer.disconnect();
  });

  function animateTestimonials() {
    testimonials.forEach((testimonial, index) => {
      setTimeout(() => {
        visibleTestimonials = [...visibleTestimonials, testimonial];
      }, index * 200);
    });
  }

  function nextSlide() {
    currentSlide = (currentSlide + 1) % Math.ceil(testimonials.length / 3);
  }

  function prevSlide() {
    currentSlide = currentSlide === 0 ? Math.ceil(testimonials.length / 3) - 1 : currentSlide - 1;
  }
</script>

<section class="testimonials" id="testimonials">
  <div class="container">
    <div class="section-header" in:fly={{ y: 50, duration: 800 }}>
      <h2>O que nossos clientes dizem</h2>
      <p>Milhares de criadores já transformaram suas comunidades em fontes de renda</p>
    </div>

    <div class="testimonials-grid">
      {#each testimonials as testimonial, index}
        {#if visibleTestimonials.includes(testimonial)}
          <div 
            class="testimonial-card"
            in:fly={{ y: 50, duration: 600, delay: index * 100 }}
          >
            <div class="testimonial-header">
              <div class="avatar">{testimonial.avatar}</div>
              <div class="user-info">
                <h4>{testimonial.name}</h4>
                <p>{testimonial.role}</p>
              </div>
              <div class="rating">
                {#each Array(testimonial.rating) as _, i}
                  <span class="star">⭐</span>
                {/each}
              </div>
            </div>
            
            <div class="testimonial-content">
              <p>"{testimonial.content}"</p>
            </div>
            
            <div class="testimonial-footer">
              <span class="revenue">Receita: {testimonial.revenue}</span>
            </div>
          </div>
        {/if}
      {/each}
    </div>

    <div class="stats-section" in:fade={{ duration: 800, delay: 1200 }}>
      <div class="stats-grid">
        <div class="stat-item">
          <div class="stat-number">98%</div>
          <div class="stat-label">Satisfação dos Clientes</div>
        </div>
        <div class="stat-item">
          <div class="stat-number">R$ 2.5M+</div>
          <div class="stat-label">Receita Gerada</div>
        </div>
        <div class="stat-item">
          <div class="stat-number">50K+</div>
          <div class="stat-label">Assinantes Ativos</div>
        </div>
        <div class="stat-item">
          <div class="stat-number">24/7</div>
          <div class="stat-label">Suporte Disponível</div>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .testimonials {
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

  .testimonials-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 2rem;
    margin-bottom: 4rem;
  }

  .testimonial-card {
    background: transparent;
    padding: 2rem;
    border-radius: 20px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
    transition: all 0.3s ease;
    border: 1px solid #e5e7eb;
  }

  .testimonial-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 12px 30px rgba(0, 0, 0, 0.1);
  }

  .testimonial-header {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-bottom: 1.5rem;
  }

  .avatar {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background: linear-gradient(135deg, #0088cc, #00a8ff);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.5rem;
    color: white;
  }

  .user-info {
    flex: 1;
  }

  .user-info h4 {
    font-size: 1.1rem;
    font-weight: 600;
    color: #1f2937;
    margin-bottom: 0.25rem;
  }

  .user-info p {
    font-size: 0.9rem;
    color: #6b7280;
  }

  .rating {
    display: flex;
    gap: 0.25rem;
  }

  .star {
    font-size: 0.875rem;
  }

  .testimonial-content {
    margin-bottom: 1.5rem;
  }

  .testimonial-content p {
    color: #374151;
    line-height: 1.6;
    font-size: 1rem;
    font-style: italic;
  }

  .testimonial-footer {
    border-top: 1px solid #e5e7eb;
    padding-top: 1rem;
  }

  .revenue {
    font-size: 0.9rem;
    font-weight: 600;
    color: #10b981;
  }

  .stats-section {
    background: linear-gradient(135deg, #0088cc, #00a8ff);
    padding: 3rem;
    border-radius: 20px;
    color: white;
  }

  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 2rem;
  }

  .stat-item {
    text-align: center;
  }

  .stat-number {
    font-size: 2.5rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
  }

  .stat-label {
    font-size: 1rem;
    opacity: 0.9;
  }

  @media (max-width: 768px) {
    .testimonials {
      padding: 4rem 1rem;
    }

    .section-header h2 {
      font-size: 2.5rem;
    }

    .section-header p {
      font-size: 1.1rem;
    }

    .testimonials-grid {
      grid-template-columns: 1fr;
      gap: 1.5rem;
    }

    .testimonial-card {
      padding: 1.5rem;
    }

    .avatar {
      width: 50px;
      height: 50px;
      font-size: 1.25rem;
    }

    .user-info h4 {
      font-size: 1rem;
    }

    .stats-section {
      padding: 2rem;
    }

    .stats-grid {
      grid-template-columns: repeat(2, 1fr);
      gap: 1.5rem;
    }

    .stat-number {
      font-size: 2rem;
    }
  }
</style> 