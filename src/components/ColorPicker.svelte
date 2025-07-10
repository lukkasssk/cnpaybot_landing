<script>
  import LordIcon from './LordIcon.svelte';
  
  let primaryColor = '#ffffff';
  let secondaryColor = '#f0f0f0';
  
  const colorOptions = [
    { name: 'Branco', value: '#ffffff' },
    { name: 'Azul', value: '#0088cc' },
    { name: 'Verde', value: '#10b981' },
    { name: 'Vermelho', value: '#ef4444' },
    { name: 'Laranja', value: '#f59e0b' },
    { name: 'Roxo', value: '#8b5cf6' },
    { name: 'Rosa', value: '#ec4899' },
    { name: 'Ciano', value: '#06b6d4' }
  ];
  
  function updateColors() {
    // Atualiza as cores dinamicamente
  }
</script>

<div class="color-picker">
  <h3>Demonstração de Cores do Lord Icon</h3>
  
  <div class="color-controls">
    <div class="color-input">
      <label for="primary">Cor Primária:</label>
      <input 
        type="color" 
        id="primary" 
        bind:value={primaryColor}
        on:input={updateColors}
      />
      <span>{primaryColor}</span>
    </div>
    
    <div class="color-input">
      <label for="secondary">Cor Secundária:</label>
      <input 
        type="color" 
        id="secondary" 
        bind:value={secondaryColor}
        on:input={updateColors}
      />
      <span>{secondaryColor}</span>
    </div>
  </div>
  
  <div class="icon-demo">
    <LordIcon 
      src="https://cdn.lordicon.com/ogjpwrxe.json"
      trigger="hover"
      colors="primary:{primaryColor},secondary:{secondaryColor}"
      size="100px"
    />
  </div>
  
  <div class="preset-colors">
    <h4>Cores Pré-definidas:</h4>
    <div class="color-grid">
      {#each colorOptions as color}
        <button 
          class="color-btn"
          style="background: {color.value}"
          on:click={() => primaryColor = color.value}
        >
          {color.name}
        </button>
      {/each}
    </div>
  </div>
  
  <div class="code-example">
    <h4>Código:</h4>
    <pre><code>&lt;LordIcon 
  src="https://cdn.lordicon.com/ogjpwrxe.json"
  trigger="hover"
  colors="primary:{primaryColor},secondary:{secondaryColor}"
  size="100px"
/&gt;</code></pre>
  </div>
</div>

<style>
  .color-picker {
    background: rgba(255, 255, 255, 0.05);
    padding: 2rem;
    border-radius: 20px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    margin-top: 2rem;
  }
  
  h3 {
    color: #ffffff;
    text-align: center;
    margin-bottom: 2rem;
  }
  
  .color-controls {
    display: flex;
    gap: 2rem;
    justify-content: center;
    margin-bottom: 2rem;
  }
  
  .color-input {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
  }
  
  .color-input label {
    color: #ffffff;
    font-size: 0.9rem;
  }
  
  .color-input input[type="color"] {
    width: 50px;
    height: 50px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
  }
  
  .color-input span {
    color: #fbfbfb;
    font-size: 0.8rem;
  }
  
  .icon-demo {
    display: flex;
    justify-content: center;
    margin: 2rem 0;
  }
  
  .preset-colors {
    margin-top: 2rem;
  }
  
  .preset-colors h4 {
    color: #ffffff;
    text-align: center;
    margin-bottom: 1rem;
  }
  
  .color-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
    gap: 1rem;
    max-width: 600px;
    margin: 0 auto;
  }
  
  .color-btn {
    padding: 0.75rem 1rem;
    border: none;
    border-radius: 8px;
    color: white;
    font-weight: 600;
    cursor: pointer;
    transition: transform 0.2s ease;
  }
  
  .color-btn:hover {
    transform: scale(1.05);
  }
  
  .code-example {
    margin-top: 2rem;
    background: rgba(0, 0, 0, 0.3);
    padding: 1rem;
    border-radius: 8px;
  }
  
  .code-example h4 {
    color: #ffffff;
    margin-bottom: 1rem;
  }
  
  pre {
    background: rgba(0, 0, 0, 0.5);
    padding: 1rem;
    border-radius: 4px;
    overflow-x: auto;
  }
  
  code {
    color: #e5e7eb;
    font-family: 'Courier New', monospace;
  }
  
  @media (max-width: 768px) {
    .color-controls {
      flex-direction: column;
      gap: 1rem;
    }
    
    .color-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }
</style> 