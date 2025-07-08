<script>
  import { onMount, afterUpdate } from 'svelte';
  import { fly, fade } from 'svelte/transition';

  let steps = [
    {
      number: '01',
      title: 'Crie sua Comunidade',
      description: 'Configure seu canal ou grupo no Telegram e conecte com nossa plataforma.',
      icon: '📱',
      color: '#0088cc'
    },
    {
      number: '02',
      title: 'Configure os Planos',
      description: 'Defina preços, períodos e benefícios dos seus planos VIP.',
      icon: '💎',
      color: '#10b981'
    },
    {
      number: '03',
      title: 'Personalize o Bot',
      description: 'Configure mensagens, regras e comportamento do seu bot de vendas.',
      icon: '🤖',
      color: '#8b5cf6'
    },
    {
      number: '04',
      title: 'Monetize',
      description: 'Comece a vender e receber pagamentos automaticamente.',
      icon: '💰',
      color: '#f59e0b'
    }
  ];

  let visibleSteps = [];
  let currentMessageIndex = 0;
  let userInput = '';
  let isBotResponding = false;
  let messages = [
    {
      type: 'received',
      text: '/start',
      time: '14:32',
      avatar: '👤'
    },
    {
      type: 'sent',
      text: 'Escolha um dos planos VIP disponíveis:',
      time: '14:32',
      avatar: '🤖'
    }
  ];

  let showPlanButtons = false;
  let planOptions = [
    { name: 'Básico', price: 'R$ 29,90/mês', icon: 'fa-solid fa-gem' },
    { name: 'Premium', price: 'R$ 49,90/mês', icon: 'fa-solid fa-star' },
    { name: 'VIP', price: 'R$ 99,90/mês', icon: 'fa-solid fa-crown' }
  ];
  let selectedPlan = null;
  let showPixButton = false;
  let showQrCode = false;
  let pixCode = '00020101021226810014br.gov.bcb.pix2559qr.woovi.com/qr/v2/cob/2365b640-748a-4ba0-8e81-b3bb70abe4bd520400005303986540549.905802BR5911CN_PAY_LTDA6009Sao_Paulo6229052595bf9c63034f4a75b7985d62663046AE6';
  let paymentApproved = false;

  let messagesContainer;
  let hasStarted = false;

  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting && !hasStarted) {
          hasStarted = true;
          animateSteps();
          startMessageAnimation();
        }
      });
    });

    const howItWorksSection = document.querySelector('.how-it-works');
    if (howItWorksSection) {
      observer.observe(howItWorksSection);
    }

    return () => observer.disconnect();
  });

  afterUpdate(() => {
    if (messagesContainer) {
      messagesContainer.scrollTop = messagesContainer.scrollHeight;
    }
  });

  function animateSteps() {
    steps.forEach((step, index) => {
      setTimeout(() => {
        visibleSteps = [...visibleSteps, step];
      }, index * 300);
    });
  }

  function startMessageAnimation() {
    currentMessageIndex = 0;
    const interval = setInterval(() => {
      if (currentMessageIndex < messages.length) {
        currentMessageIndex++;
        if (currentMessageIndex === 2) {
          setTimeout(() => {
            addPlanToggleMessage();
          }, 600);
        }
      } else {
        clearInterval(interval);
      }
    }, 1200);
  }

  function addPlanToggleMessage() {
    messages = [
      ...messages,
      {
        type: 'plan-toggle',
        time: '',
        avatar: '🤖',
        html: false
      }
    ];
    currentMessageIndex = messages.length;
  }

  function selectPlan(plan) {
    selectedPlan = plan.name;
    // Adiciona mensagem de resumo do plano
    const now = new Date();
    const hora = now.getHours().toString().padStart(2, '0') + ':' + now.getMinutes().toString().padStart(2, '0');
    let duration = '';
    if (plan.name === 'Básico') duration = '30 dias';
    if (plan.name === 'Premium') duration = '60 dias';
    if (plan.name === 'VIP') duration = '90 dias';
    let resumo = `<span class='translatable-message'>
      <i class='fa-solid fa-gem'></i> Plano: <b>${plan.name}</b><br>
      <i class='fa-solid fa-money-bill-wave'></i> Valor: ${plan.price}<br>
      <i class='fa-solid fa-clock'></i> Duração: ${duration}<br><br>
      <strong>DEMO</strong>: Nenhum pagamento é real.
    </span>`;
    messages = [
      ...messages,
      {
        type: 'sent',
        html: true,
        text: resumo,
        time: hora,
        avatar: '🤖',
        isPlanSummary: true,
        showPixButton: true
      }
    ];
    currentMessageIndex = messages.length;
    showPlanButtons = false;
  }

  function sendUserMessage() {
    if (!userInput.trim() || isBotResponding) return;
    const now = new Date();
    const hora = now.getHours().toString().padStart(2, '0') + ':' + now.getMinutes().toString().padStart(2, '0');
    messages = [
      ...messages,
      {
        type: 'received',
        text: userInput,
        time: hora,
        avatar: '👤',
        html: false
      }
    ];
    currentMessageIndex = messages.length;
    userInput = '';
    isBotResponding = true;
    setTimeout(() => {
      botAutoReply();
    }, 1200);
  }

  function botAutoReply() {
    const now = new Date();
    const hora = now.getHours().toString().padStart(2, '0') + ':' + now.getMinutes().toString().padStart(2, '0');
    const replies = [
      'Olá! Como posso ajudar você hoje?',
      'Para ver os planos, digite /planos.',
      'Se precisar de suporte, digite /suporte.',
      'Obrigado por entrar em contato!'
    ];
    const reply = replies[Math.floor(Math.random() * replies.length)];
    messages = [
      ...messages,
      {
        type: 'sent',
        text: reply,
        time: hora,
        avatar: '🤖',
        html: false
      }
    ];
    currentMessageIndex = messages.length;
    isBotResponding = false;
  }

  function generatePix() {
    showQrCode = true;
    const now = new Date();
    const hora = now.getHours().toString().padStart(2, '0') + ':' + now.getMinutes().toString().padStart(2, '0');
    const valorPix = 'R$ 0,01';
    const mensagemPix = `
      <div style='text-align:left;'>
        <b>Escaneie o QR Code abaixo para pagar automaticamente:</b><br><br>
        💰 <b>Valor:</b> ${valorPix}<br><br>
        <b>📋 Código PIX para copiar:</b><br>
        <code style='font-size:11px;word-break:break-all;'>${pixCode}</code><br><br>
        <b>📱 Como pagar:</b><br>
        1. Escaneie o QR Code acima, OU<br>
        2. Copie o código PIX acima e cole no app do seu banco<br><br>
        ⏳ <b>Aguardando pagamento...</b>
      </div>
    `;
    messages = [
      ...messages,
      {
        type: 'sent',
        html: true,
        text: mensagemPix,
        time: hora,
        avatar: '🤖',
        showQrCode: true
      }
    ];
    currentMessageIndex = messages.length;
    // Auto aprova o pagamento após 5 segundos
    setTimeout(() => {
      approvePayment();
    }, 5000);
  }

  function approvePayment() {
    paymentApproved = true;
    const now = new Date();
    const hora = now.getHours().toString().padStart(2, '0') + ':' + now.getMinutes().toString().padStart(2, '0');
    
    messages = [
      ...messages,
      {
        type: 'sent',
        text: '✅ Pagamento aprovado! Seu acesso foi liberado.',
        time: hora,
        avatar: '🤖',
        html: false
      }
    ];
    currentMessageIndex = messages.length;
  }
</script>

<section class="how-it-works" id="how-it-works">
  <div class="container">


    <div class="demo-section" in:fade={{ duration: 800, delay: 1200 }}>
      <div class="demo-content">
        <h3>Veja em Ação</h3>
        <p>Confira como é fácil configurar e usar nossa plataforma</p>
        
        <div class="phone-container">
          <div class="phone-frame">
            <div class="phone-screen">
              <!-- Header do Telegram -->
              <div class="telegram-header">
                <div class="header-content">
                  <div class="back-button"><i class="fa-solid fa-arrow-left"></i></div>
                  <div class="chat-info">
                    <div class="chat-avatar"><img src="../../static/imagem/cn_logo.jpg" alt="avatar"></div>
                    <div class="chat-details">
                      <div class="chat-name">Bot CnPay</div>
                      <div class="chat-status">online</div>
                    </div>
                  </div>
                  <div class="header-actions">
                    <div class="action-btn"><i class="fa-solid fa-phone"></i></div>
                    <div class="action-btn"><i class="fa-solid fa-ellipsis-v"></i></div>
                  </div>
                </div>
              </div>

              <!-- Área de mensagens -->
              <div class="messages-container" bind:this={messagesContainer}>
                {#each messages as message, index}
                  {#if index < currentMessageIndex}
                    {#if message.type === 'plan-toggle'}
                      <div class="message sent" in:fly={{ y: 20, duration: 500, delay: index * 200 }}>
                        <div class="message-avatar"><img src="../../static/imagem/cn_logo.jpg" alt="avatar"></div>
                        <div class="plan-bubble {selectedPlan ? 'selected' : ''}">
                          <div class="plan-buttons">
                            {#each planOptions as plan}
                              <button class="plan-btn {selectedPlan === plan.name ? 'selected' : ''}" on:click={() => selectPlan(plan)}>
                                <span class="plan-icon"><i class="{plan.icon}"></i></span>
                                <span class="plan-name">{plan.name}</span>
                                <span class="plan-price">{plan.price}</span>
                              </button>
                            {/each}
                          </div>
                          {#if selectedPlan}
                            <div class="plan-selected-msg">Você selecionou: <b>{selectedPlan}</b></div>
                          {/if}
                        </div>
                      </div>
                    {:else}
                      <div class="message {message.type} {message.isPlanSummary ? 'spoilers-container' : ''}" in:fly={{ y: 20, duration: 500, delay: index * 200 }}>
                        <div class="message-avatar">
                          {#if message.avatar && message.avatar !== '🤖'}
                            {message.avatar}
                          {:else}
                            <img src="../../static/imagem/cn_logo.jpg" alt="avatar">
                          {/if}
                        </div>
                        <div class="message-bubble {message.isPlanSummary ? 'bubble-content-wrapper' : ''}">
                          <div class="bubble-content">
                            {#if message.isPlanSummary}
                              <span class="translatable-message">{@html message.text}</span>
                              <div class="reply-markup">
                                <div class="reply-markup-row">
                                  <button class="reply-markup-button rp" on:click={() => generatePix()}>
                                    <span class="reply-markup-button-text">
                                      <i class="fa-solid fa-qrcode"></i> Gerar PIX
                                    </span>
                                  </button>
                                </div>
                              </div>
                            {:else if message.html}
                              <span class="translatable-message">{@html message.text}</span>
                            {:else}
                              <div class="message-text">{message.text}</div>
                            {/if}
                            <span class="time">{message.time}</span>
                            {#if message.showQrCode}
                              <div class="qr-code-container">
                                <div class="qr-code">
                                  <div class="qr-code-placeholder">
                                    <i class="fa-solid fa-qrcode"></i>
                                    <span>QR Code PIX</span>
                                  </div>
                                </div>
                                <div class="pix-code">
                                  <span>Código PIX:</span>
                                  <code>{pixCode}</code>
                                </div>
                              </div>
                            {/if}
                          </div>
                          <div class="bubble-tail {message.type}"></div>
                        </div>
                      </div>
                    {/if}
                  {/if}
                {/each}
              </div>

              <!-- Área de digitação -->
              <div class="input-area">
                <div class="input-container">
                  <div class="input-actions">
                    <div class="action-icon"><i class="fa-solid fa-paperclip"></i></div>
                    <div class="action-icon"><i class="fa-regular fa-face-smile"></i></div>
                  </div>
                  <div class="text-input">
                    <input
                      type="text"
                      placeholder="Digite uma mensagem..."
                      bind:value={userInput}
                      on:keydown={(e) => { if (e.key === 'Enter') sendUserMessage(); }}
                      autocomplete="off"
                    />
                  </div>
                  <div class="send-button" on:click={sendUserMessage} style="cursor:pointer;"><i class="fa-solid fa-paper-plane"></i></div>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Botão CRIAR MEU BOT -->
        <div class="demo-button-container">
          <button class="btn-primary s-9RSm83WgTQHR">
            VER BOT DEMO
          </button>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .how-it-works {
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

  .steps-container {
    position: relative;
    margin-bottom: 4rem;
  }

  .steps-line {
    position: absolute;
    top: 100px;
    left: 50%;
    transform: translateX(-50%);
    width: 2px;
    height: calc(100% - 200px);
    background: linear-gradient(180deg, #e5e7eb 0%, #0088cc 50%, #e5e7eb 100%);
    z-index: 1;
  }

  .step-card {
    display: flex;
    align-items: center;
    gap: 2rem;
    margin-bottom: 3rem;
    position: relative;
    z-index: 2;
  }

  .step-card:nth-child(even) {
    flex-direction: row-reverse;
  }

  .step-number {
    font-size: 4rem;
    font-weight: 900;
    color: #f3f4f6;
    line-height: 1;
    position: absolute;
    top: -20px;
    left: 50%;
    transform: translateX(-50%);
    z-index: 3;
  }

  .step-icon {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 3rem;
    color: white;
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
    position: relative;
    z-index: 4;
    transition: transform 0.3s ease;
  }

  .step-card:hover .step-icon {
    transform: scale(1.1);
  }

  .step-content {
    flex: 1;
    max-width: 400px;
  }

  .step-content h3 {
    font-size: 1.75rem;
    font-weight: 600;
    color: #1f2937;
    margin-bottom: 1rem;
  }

  .step-content p {
    color: #6b7280;
    line-height: 1.6;
    font-size: 1.1rem;
  }

  .demo-section {
    text-align: center;
    background: transparent;
    padding: 0rem 3rem 3rem 3rem;
    border-radius: 20px;
  }

  .demo-content h3 {
    font-size: 2rem;
    font-weight: 700;
    color:rgb(255, 255, 255);
    margin-bottom: 1rem;
  }

  .demo-content p {
    color: #6b7280;
    font-size: 1.1rem;
    margin-bottom: 2rem;
  }

  .phone-container {
    display: flex;
    justify-content: center;
    margin-top: 2rem;
  }

  .demo-button-container {
    display: flex;
    justify-content: center;
    margin-top: 3rem;
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

  .phone-frame {
    width: 320px;
    height: 600px;
    background: #1a1a1a;
    border-radius: 30px;
    padding: 8px;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
    position: relative;
  }

  .phone-frame::before {
    content: '';
    position: absolute;
    top: 15px;
    left: 50%;
    transform: translateX(-50%);
    width: 60px;
    height: 4px;
    background: #333;
    border-radius: 2px;
  }

  .phone-screen {
    width: 100%;
    height: 100%;
    background: url(/static/imagem/background_telegram.jpg) repeat center center #222b33;
    border-radius: 22px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
  }

  .telegram-header {
    background: #202021;
    color: white;
    padding: 14px 18px 12px 18px;
    position: relative;
    box-shadow: 0 2px 8px rgba(0,0,0,0.07);
    border-top-left-radius: 22px;
    border-top-right-radius: 22px;
    backdrop-filter: blur(10px);
  }

  .header-content {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 16px;
  }

  .back-button {
    font-size: 22px;
    font-weight: bold;
    cursor: pointer;
    display: flex;
    align-items: center;
  }

  .chat-info {
    display: flex;
    align-items: center;
    gap: 12px;
    flex: none;
    margin-left: 0;
  }

  .chat-avatar {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    border: 2px solid #fff;
    box-shadow: 0 1px 4px rgba(0,0,0,0.08);
  }

  .chat-avatar img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
    border-radius: 50%;
    box-shadow: none;
    border: none;
  }

  .chat-details {
    flex: 1;
  }

  .chat-name {
    font-weight: 600;
    font-size: 16px;
  }

  .chat-status {
    font-size: 12px;
    opacity: 0.8;
  }

  .header-actions {
    display: flex;
    gap: 16px;
    margin-left: 12px;
  }

  .action-btn {
    font-size: 18px;
    cursor: pointer;
    display: flex;
    align-items: center;
  }

  .messages-container {
    flex: 1;
    max-height: 460px;
    height: 100%;
    padding: 18px 10px 12px 10px;
    background-position: center;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    gap: 14px;
  }

  .message {
    display: flex;
    gap: 8px;
    max-width: 80%;
  }

  .message.received {
    align-self: flex-start;
  }

  .message.sent {
    align-self: flex-end;
    flex-direction: row-reverse;
  }
  .message-avatar img {
    object-fit: cover;
    width: 32px;
    border-radius: 50%; 
    height: 32px;
  }
  .message-avatar {
    width: 32px;
    height: 32px;
    border-radius: 50%;
    background: #ffffff;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 14px;
    flex-shrink: 0;
  }

  .message-bubble {
    position: relative;
    --bubble-bg: #292730ab;
    background: var(--bubble-bg);
    border-radius: 18px;
    overflow: visible;
    padding: 12px 16px;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.08);
    color: rgb(255, 255, 255);
  }

  .plan-bubble.selected {
    --bubble-bg: hsl(284.82deg 49.74% 37.6% / 40%);
    color: #fff;
  }

  .bubble-tail {
    position: absolute;
    bottom: 0;
    width: 16px;
    height: 16px;
    overflow: hidden;
    z-index: 2;
    pointer-events: none;
  }

  .message.received .bubble-tail {
    left: -14px;
  }

  .message.sent .bubble-tail {
    right: -14px;
    transform: scaleX(-1);
  }

  .bubble-tail::after {
    content: '';
    display: block;
    width: 16px;
    height: 16px;
    background: var(--bubble-bg);
    border-bottom-left-radius: 16px;
    position: absolute;
    left: 0;
    bottom: 0;
    box-shadow: 0 1px 2px rgba(0,0,0,0.08);
  }

  .message-text {
    font-size: 13px;
    text-align: start;
    line-height: 1.4;
    white-space: pre-line;
  }

  .message-time {
    font-size: 11px;
    opacity: 0.7;
    margin-top: 4px;
    text-align: right;
  }

  .input-area {
    position: absolute;
    bottom: 0;
    background: transparent;
    padding: 12px 16px;
  }

  .input-container {
    display: flex;
    align-items: center;
    gap: 12px;
    background: #292730ab;
    border-radius: 24px;
    padding: 8px 16px;
  }

  .input-actions {
    display: flex;
    gap: 8px;
    color: white;
  }

  .action-icon {
    font-size: 18px;
    cursor: pointer;
    opacity: 0.7;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .text-input {
    flex: 1;
    color: #fff;
    font-size: 14px;
    background: transparent;
    border: none;
    outline: none;
    padding: 0;
  }

  .text-input input {
    width: 100%;
    background: transparent;
    border: none;
    color: #fff;
    font-size: 14px;
    outline: none;
    padding: 0;
  }

  .send-button {
    width: 32px;
    height: 32px;
    border-radius: 50%;
    background: #0088cc;
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 18px;
    cursor: pointer;
  }

  .plan-bubble {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    transition: background 0.2s, color 0.2s;
  }

  .plan-buttons {
    display: flex;
    background: transparent;
    gap: 8px;
    margin-bottom: 6px;
    flex-wrap: wrap;
  }

  .plan-btn {
    display: flex;
    align-items: center;
    border-radius: .375rem;
    gap: 6px;
    outline: none;
    border: none;
    cursor: pointer;
    background: hsl(284.82deg 49.74% 37.6% / 40%);
    width: 100%;
    color: #fff;
    padding: 7px 14px;
    font-size: 14px;
    font-weight: 500;
    cursor: pointer;
    transition: background 0.2s, color 0.2s;
    outline: none;
  }

  .plan-btn.selected, .plan-btn:hover {
    background: hsl(284.82deg 49.74% 37.6% / 40%) !important;
    color: #fff !important;
    border-color: hsl(284.82deg 49.74% 37.6%);
  }

  .plan-icon {
    font-size: 18px;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 22px;
  }

  .plan-name {
    font-weight: 600;
  }

  .plan-price {
    font-size: 13px;
    opacity: 0.8;
    margin-left: 4px;
  }

  .plan-selected-msg {
    margin-top: 6px;
    font-size: 13px;
    color: #229ED9;
  }

  @media (max-width: 768px) {
    .how-it-works {
      padding: 0rem 1rem;
    }
    .btn-primary{
      padding: 1rem;
    }

    .section-header h2 {
      font-size: 2.5rem;
    }

    .section-header p {
      font-size: 1.1rem;
    }

    .steps-line {
      display: none;
    }

    .step-card {
      flex-direction: column !important;
      text-align: center;
      gap: 1.5rem;
    }

    .step-number {
      position: static;
      transform: none;
      font-size: 3rem;
      margin-bottom: 1rem;
    }

    .step-icon {
      width: 100px;
      height: 100px;
      font-size: 2.5rem;
    }

    .step-content {
      max-width: none;
    }

    .step-content h3 {
      font-size: 1.5rem;
    }

    .demo-section {
      padding: 2rem;
    }

    .demo-content h3 {
      font-size: 1.75rem;
    }

    .phone-frame {
      width: 280px;
      height: 520px;
    }
  }

  /* Spoilers/Resumo do Plano */
  .spoilers-container {
    margin-top: 8px;
  }
  .bubble-content {
    display: flex;
    flex-direction: column;
    gap: 6px;
  }
  .translatable-message {
    font-size: 13px;
    text-align: start;
    line-height: 1.5;
    display: block;
  }
  .bubble-content .time {
    font-size: 11px;
    opacity: 0.7;
    margin-top: 4px;
    text-align: right;
    align-self: flex-end;
  }
  .reply-markup {
    margin-top: 8px;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
  }
  .reply-markup-row {
    display: flex;
    gap: 8px;
  }
  .reply-markup-button {
    background: hsl(284.82deg 49.74% 37.6% / 40%);
    color: #fff;
    border: none;
    border-radius: 16px;
    padding: 7px 18px;
    font-size: 14px;
    font-weight: 500;
    cursor: pointer;
    transition: background 0.2s;
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .reply-markup-button:hover {
    background: hsl(284.82deg 49.74% 37.6% / 60%);
  }

  .reply-markup-button-text {
    display: flex;
    align-items: center;
    gap: 6px;
  }

  /* QR Code Styles */
  .qr-code-container {
    margin-top: 12px;
    display: flex;
    flex-direction: column;
    gap: 8px;
    align-items: center;
  }

  .qr-code {
    background: white;
    border-radius: 8px;
    padding: 16px;
    display: flex;
    align-items: center;
    justify-content: center;
    min-width: 120px;
    min-height: 120px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }

  .qr-code-placeholder {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    color: #666;
    font-size: 12px;
  }

  .qr-code-placeholder i {
    font-size: 48px;
    color: #0088cc;
  }

  .pix-code {
    display: flex;
    flex-direction: column;
    gap: 4px;
    font-size: 11px;
    color: #fff;
    opacity: 0.8;
    text-align: center;
  }

  .pix-code code {
    background: rgba(255, 255, 255, 0.1);
    padding: 4px 8px;
    border-radius: 4px;
    font-family: monospace;
    font-size: 10px;
    word-break: break-all;
    max-width: 200px;
  }
</style> 