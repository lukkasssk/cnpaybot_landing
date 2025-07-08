<script>
  import LordIcon from './LordIcon.svelte';
  
  // Lista de ícones populares do Lord Icon
  const icons = [
    {
      name: 'QR Code',
      src: 'https://cdn.lordicon.com/avwubsdy.json',
      description: 'Ícone de QR Code animado'
    },
    {
      name: 'Telegram',
      src: 'https://cdn.lordicon.com/avwubsdy.json',
      description: 'Ícone do Telegram'
    },
    {
      name: 'Payment',
      src: 'https://cdn.lordicon.com/avwubsdy.json',
      description: 'Ícone de pagamento'
    },
    {
      name: 'Success',
      src: 'https://cdn.lordicon.com/avwubsdy.json',
      description: 'Ícone de sucesso'
    }
  ];
</script>

<section class="lord-icon-demo">
  <div class="container">
    <h2>Demonstração dos Ícones Lord Icon</h2>
    <p>Exemplos de como usar os ícones animados do Lord Icon em seu projeto</p>
    
    <div class="icons-grid">
      {#each icons as icon}
        <div class="icon-card">
          <LordIcon 
            src={icon.src}
            trigger="hover"
            colors="primary:#0088cc,secondary:#00a8ff"
            size="80px"
          />
          <h3>{icon.name}</h3>
          <p>{icon.description}</p>
        </div>
      {/each}
    </div>
    
    <div class="usage-examples">
      <h3>Exemplos de Uso</h3>
      
      <div class="example">
        <h4>Ícone com Trigger Hover</h4>
        <LordIcon 
          src="https://cdn.lordicon.com/avwubsdy.json"
          trigger="hover"
          colors="primary:#0088cc,secondary:#00a8ff"
          size="60px"
        />
        <code>trigger="hover"</code>
      </div>
      
      <div class="example">
        <h4>Ícone com Trigger Click</h4>
        <LordIcon 
          src="https://cdn.lordicon.com/avwubsdy.json"
          trigger="click"
          colors="primary:#10b981,secondary:#34d399"
          size="60px"
        />
        <code>trigger="click"</code>
      </div>
      
      <div class="example">
        <h4>Ícone com Loop</h4>
        <LordIcon 
          src="https://cdn.lordicon.com/avwubsdy.json"
          trigger="loop"
          colors="primary:#f59e0b,secondary:#fbbf24"
          size="60px"
        />
        <code>trigger="loop"</code>
      </div>
    </div>
  </div>
</section>

<style>
  .lord-icon-demo {
    padding: 4rem 0;
    background: #f8fafc;
  }
  
  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
  }
  
  h2 {
    text-align: center;
    font-size: 2.5rem;
    color: #1f2937;
    margin-bottom: 1rem;
  }
  
  p {
    text-align: center;
    color: #6b7280;
    margin-bottom: 3rem;
  }
  
  .icons-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
    margin-bottom: 4rem;
  }
  
  .icon-card {
    background: white;
    padding: 2rem;
    border-radius: 12px;
    text-align: center;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
    transition: transform 0.3s ease;
  }
  
  .icon-card:hover {
    transform: translateY(-4px);
  }
  
  .icon-card h3 {
    margin: 1rem 0 0.5rem;
    color: #1f2937;
  }
  
  .icon-card p {
    color: #6b7280;
    font-size: 0.9rem;
  }
  
  .usage-examples {
    background: white;
    padding: 2rem;
    border-radius: 12px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  }
  
  .usage-examples h3 {
    text-align: center;
    margin-bottom: 2rem;
    color: #1f2937;
  }
  
  .example {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-bottom: 1.5rem;
    padding: 1rem;
    background: #f8fafc;
    border-radius: 8px;
  }
  
  .example h4 {
    min-width: 150px;
    color: #374151;
    font-size: 0.9rem;
  }
  
  .example code {
    background: #e5e7eb;
    padding: 0.25rem 0.5rem;
    border-radius: 4px;
    font-size: 0.8rem;
    color: #374151;
  }
  
  @media (max-width: 768px) {
    .icons-grid {
      grid-template-columns: 1fr;
    }
    
    .example {
      flex-direction: column;
      text-align: center;
    }
    
    .example h4 {
      min-width: auto;
    }
  }
</style> 