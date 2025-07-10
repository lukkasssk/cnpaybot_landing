<script>
  let openItem = null;

  const faqItems = [
    {
      id: 1,
      question: "Preciso saber programar?",
      answer: "Não! Nossa plataforma é totalmente intuitiva e não requer conhecimento técnico. Você pode configurar seu bot em poucos minutos."
    },
    {
      id: 2,
      question: "O dinheiro vai direto para minha conta?",
      answer: "Sim! Todos os pagamentos são processados diretamente para sua conta bancária ou carteira digital, sem intermediários."
    },
    {
      id: 3,
      question: "O bot remove automaticamente quem não pagar?",
      answer: "Sim! O bot possui sistema automático que remove usuários que não efetuaram o pagamento dentro do prazo estipulado."
    },
    {
      id: 4,
      question: "Posso criar mais de um bot?",
      answer: "Claro! Você pode criar quantos bots precisar para diferentes projetos ou negócios, tudo gerenciado em uma única conta."
    },
    {
      id: 5,
      question: "E se eu tiver problemas?",
      answer: "Nossa equipe de suporte está disponível 24/7 para ajudar com qualquer dúvida ou problema que você possa ter."
    }
  ];

  function toggleItem(id) {
    openItem = openItem === id ? null : id;
  }
</script>

<section id="faq" class="py-32">
  <div class="mx-auto max-w-6xl px-4 md:px-6 space-y-16">
    <div class="mx-auto flex max-w-5xl flex-col text-left md:text-center">
      <h2 class="mb-3 text-3xl font-semibold md:mb-4 lg:mb-6 lg:text-4xl">
        Perguntas frequentes
      </h2>
      <p class="text-muted-foreground lg:text-lg">
        Tudo que você precisa saber sobre a plataforma. Não encontrou a resposta? Fale com nosso suporte!
      </p>
    </div>

    <div class="mx-auto w-full max-w-5xl">
      {#each faqItems as item}
        <div class="border-t border-white/10">
          <h3 class="flex">
            <button 
              type="button" 
              class="flex flex-1 items-start justify-between gap-4 rounded-md py-4 text-left text-sm font-medium outline-none transition-opacity duration-200 hover:no-underline hover:opacity-60"
              on:click={() => toggleItem(item.id)}
            >
              <div class="font-medium sm:py-1 lg:py-2 lg:text-lg">
                {item.question}
              </div>
              <svg 
                xmlns="http://www.w3.org/2000/svg" 
                width="24" 
                height="24" 
                viewBox="0 0 24 24" 
                fill="none" 
                stroke="currentColor" 
                stroke-width="2" 
                stroke-linecap="round" 
                stroke-linejoin="round" 
                class="lucide lucide-chevron-down text-muted-foreground pointer-events-none size-4 shrink-0 translate-y-0.5 transition-transform duration-200 {openItem === item.id ? 'rotate-180' : ''}"
                aria-hidden="true"
              >
                <path d="m6 9 6 6 6-6"></path>
              </svg>
            </button>
          </h3>
          <div class="overflow-hidden text-sm transition-all duration-200 {openItem === item.id ? 'max-h-96 opacity-100' : 'max-h-0 opacity-0'}">
            <div class="py-4 text-muted-foreground">
              {item.answer}
            </div>
          </div>
        </div>
      {/each}
    </div>

    <div class="mx-auto flex max-w-4xl flex-col items-center rounded-lg bg-accent p-4 text-center md:rounded-xl md:p-6 lg:p-8" id="suporte">
      <div class="relative">
        <span class="flex shrink-0 overflow-hidden rounded-full absolute mb-4 size-16 origin-bottom -translate-x-[60%] scale-[80%] border md:mb-5">
          <img class="aspect-square size-full" src="https://shadcnblocks.com/images/block/avatar-2.webp" alt="Suporte 1">
        </span>
        <span class="flex shrink-0 overflow-hidden rounded-full absolute mb-4 size-16 origin-bottom translate-x-[60%] scale-[80%] border md:mb-5">
          <img class="aspect-square size-full" src="https://shadcnblocks.com/images/block/avatar-3.webp" alt="Suporte 2">
        </span>
        <span class="relative flex shrink-0 overflow-hidden rounded-full mb-4 size-16 border md:mb-5">
          <img class="aspect-square size-full" src="https://shadcnblocks.com/images/block/avatar-1.webp" alt="Suporte 3">
        </span>
      </div>
      <h3 class="mb-2 max-w-3xl font-semibold lg:text-lg">
        Ainda com dúvidas?
      </h3>
      <p class="mb-8 max-w-3xl text-muted-foreground lg:text-lg">
        Não encontrou a resposta? Fale com nosso suporte!
      </p>
      <div class="flex w-full flex-col justify-center gap-2 sm:flex-row">
        <a 
          href="https://t.me/cnpayy_bot" 
          target="_blank" 
          class="inline-flex items-center justify-center whitespace-nowrap rounded-md text-sm font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 bg-primary text-primary-foreground hover:bg-primary/90 h-10 px-4 py-2 w-full sm:w-auto"
        >
          Falar com Gerente
        </a>
      </div>
    </div>
  </div>
</section>

<style>
  :global(.text-muted-foreground) {
    color: #fbfbfb;
  }

  :global(.bg-accent) {
    background-color: rgba(255, 255, 255, 0.05);
  }

  :global(.bg-primary) {
    background-color: #0088cc;
  }

  :global(.text-primary-foreground) {
    color: white;
  }

  :global(.hover\:bg-primary\/90:hover) {
    background-color: rgba(0, 136, 204, 0.9);
  }

  :global(.border) {
    border-color: rgba(255, 255, 255, 0.1);
  }

  :global(.border-b) {
    border-bottom-color: rgba(255, 255, 255, 0.1);
  }

  :global(.border-t) {
    border-top-width: 1px;
  }

  :global(.border-white\/10) {
    border-color: rgba(255, 255, 255, 0.1);
  }

  :global(.text-3xl) {
    font-size: 1.875rem;
    line-height: 2.25rem;
  }

  :global(.text-4xl) {
    font-size: 2.25rem;
    line-height: 2.5rem;
  }

  :global(.lg\:text-4xl) {
    @media (min-width: 1024px) {
      font-size: 2.25rem;
      line-height: 2.5rem;
    }
  }

  :global(.lg\:text-lg) {
    @media (min-width: 1024px) {
      font-size: 1.125rem;
      line-height: 1.75rem;
    }
  }

  :global(.py-32) {
    padding-top: 8rem;
    padding-bottom: 8rem;
  }

  :global(.max-w-6xl) {
    max-width: 72rem;
  }

  :global(.max-w-5xl) {
    max-width: 64rem;
  }

  :global(.max-w-4xl) {
    max-width: 56rem;
  }

  :global(.px-4) {
    padding-left: 1rem;
    padding-right: 1rem;
  }

  :global(.md\:px-6) {
    @media (min-width: 768px) {
      padding-left: 1.5rem;
      padding-right: 1.5rem;
    }
  }

  :global(.space-y-16 > * + *) {
    margin-top: 4rem;
  }

  :global(.mb-3) {
    margin-bottom: 0.75rem;
  }

  :global(.md\:mb-4) {
    @media (min-width: 768px) {
      margin-bottom: 1rem;
    }
  }

  :global(.lg\:mb-6) {
    @media (min-width: 1024px) {
      margin-bottom: 1.5rem;
    }
  }

  :global(.font-semibold) {
    font-weight: 600;
  }

  :global(.rounded-lg) {
    border-radius: 0.5rem;
  }

  :global(.md\:rounded-xl) {
    @media (min-width: 768px) {
      border-radius: 0.75rem;
    }
  }

  :global(.p-4) {
    padding: 1rem;
  }

  :global(.md\:p-6) {
    @media (min-width: 768px) {
      padding: 1.5rem;
    }
  }

  :global(.lg\:p-8) {
    @media (min-width: 1024px) {
      padding: 2rem;
    }
  }

  :global(.mb-4) {
    margin-bottom: 1rem;
  }

  :global(.md\:mb-5) {
    @media (min-width: 768px) {
      margin-bottom: 1.25rem;
    }
  }

  :global(.mb-2) {
    margin-bottom: 0.5rem;
  }

  :global(.mb-8) {
    margin-bottom: 2rem;
  }

  :global(.size-16) {
    width: 4rem;
    height: 4rem;
  }

  :global(.gap-2) {
    gap: 0.5rem;
  }

  :global(.sm\:flex-row) {
    @media (min-width: 640px) {
      flex-direction: row;
    }
  }

  :global(.h-10) {
    height: 2.5rem;
  }

  :global(.px-4) {
    padding-left: 1rem;
    padding-right: 1rem;
  }

  :global(.py-2) {
    padding-top: 0.5rem;
    padding-bottom: 0.5rem;
  }

  :global(.w-full) {
    width: 100%;
  }

  :global(.sm\:w-auto) {
    @media (min-width: 640px) {
      width: auto;
    }
  }

  :global(.text-sm) {
    font-size: 0.875rem;
    line-height: 1.25rem;
  }

  :global(.font-medium) {
    font-weight: 500;
  }

  :global(.py-4) {
    padding-top: 1rem;
    padding-bottom: 1rem;
  }

  :global(.sm\:py-1) {
    @media (min-width: 640px) {
      padding-top: 0.25rem;
      padding-bottom: 0.25rem;
    }
  }

  :global(.lg\:py-2) {
    @media (min-width: 1024px) {
      padding-top: 0.5rem;
      padding-bottom: 0.5rem;
    }
  }

  :global(.lg\:text-lg) {
    @media (min-width: 1024px) {
      font-size: 1.125rem;
      line-height: 1.75rem;
    }
  }

  :global(.size-4) {
    width: 1rem;
    height: 1rem;
  }

  :global(.translate-y-0\.5) {
    transform: translateY(0.125rem);
  }

  :global(.transition-transform) {
    transition-property: transform;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    transition-duration: 150ms;
  }

  :global(.duration-200) {
    transition-duration: 200ms;
  }

  :global(.rotate-180) {
    transform: rotate(180deg);
  }

  #faq > div > div > div{
    display: flex;
    background: transparent;
    flex-direction: column;
    color: white;
    gap: 0.4rem;
  }

  a{
    text-decoration: none;
  }

  #faq > div > div > div > h3 > button{
    background: #ffffff3d;
    color: white;
    align-items: center;
    padding: 10px;
    border: 1px solid #ffffff24;
  }

  :global(.max-h-96) {
    max-height: 24rem;
  }

  :global(.max-h-0) {
    max-height: 0px;
  }

  :global(.opacity-100) {
    opacity: 1;
  }

  :global(.opacity-0) {
    opacity: 0;
  }

  :global(.transition-all) {
    transition-property: all;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    transition-duration: 150ms;
  }

  :global(.overflow-hidden) {
    overflow: hidden;
  }

  :global(.pointer-events-none) {
    pointer-events: none;
  }

  :global(.shrink-0) {
    flex-shrink: 0;
  }

  :global(.rounded-full) {
    border-radius: 9999px;
  }

  :global(.absolute) {
    position: absolute;
  }

  :global(.relative) {
    position: relative;
  }

  :global(.origin-bottom) {
    transform-origin: bottom;
  }

  :global(.-translate-x-\[60\%\]) {
    transform: translateX(-60%);
  }

  :global(.translate-x-\[60\%\]) {
    transform: translateX(60%);
  }

  :global(.scale-\[80\%\]) {
    transform: scale(0.8);
  }

  :global(.border) {
    border-width: 1px;
  }

  :global(.aspect-square) {
    aspect-ratio: 1 / 1;
  }

  :global(.max-w-3xl) {
    max-width: 48rem;
  }

  :global(.inline-flex) {
    display: inline-flex;
  }

  :global(.items-center) {
    align-items: center;
  }

  :global(.justify-center) {
    justify-content: center;
  }

  :global(.whitespace-nowrap) {
    white-space: nowrap;
  }

  :global(.ring-offset-background) {
    --tw-ring-offset-color: hsl(var(--background));
  }

  :global(.transition-colors) {
    transition-property: color, background-color, border-color, text-decoration-color, fill, stroke;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    transition-duration: 150ms;
  }

  :global(.focus-visible\:outline-none:focus-visible) {
    outline: 2px solid transparent;
    outline-offset: 2px;
  }

  :global(.focus-visible\:ring-2:focus-visible) {
    --tw-ring-offset-shadow: var(--tw-ring-inset) 0 0 0 var(--tw-ring-offset-width) var(--tw-ring-offset-color);
    --tw-ring-shadow: var(--tw-ring-inset) 0 0 0 calc(2px + var(--tw-ring-offset-width)) var(--tw-ring-color);
    box-shadow: var(--tw-ring-offset-shadow), var(--tw-ring-shadow), var(--tw-shadow, 0 0 #0000);
  }

  :global(.focus-visible\:ring-ring:focus-visible) {
    --tw-ring-color: hsl(var(--ring));
  }

  :global(.focus-visible\:ring-offset-2:focus-visible) {
    --tw-ring-offset-width: 2px;
  }

  :global(.disabled\:pointer-events-none:disabled) {
    pointer-events: none;
  }

  :global(.disabled\:opacity-50:disabled) {
    opacity: 0.5;
  }

  :global(.hover\:no-underline:hover) {
    text-decoration: none;
  }

  :global(.hover\:opacity-60:hover) {
    opacity: 0.6;
  }

  :global(.flex) {
    display: flex;
  }

  :global(.flex-1) {
    flex: 1 1 0%;
  }

  :global(.items-start) {
    align-items: flex-start;
  }

  :global(.justify-between) {
    justify-content: space-between;
  }

  :global(.gap-4) {
    gap: 1rem;
  }

  :global(.rounded-md) {
    border-radius: 0.375rem;
  }

  :global(.text-left) {
    text-align: left;
  }

  :global(.outline-none) {
    outline: 2px solid transparent;
    outline-offset: 2px;
  }

  :global(.transition-opacity) {
    transition-property: opacity;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    transition-duration: 150ms;
  }

  :global(.flex-col) {
    flex-direction: column;
  }

  :global(.md\:text-center) {
    @media (min-width: 768px) {
      text-align: center;
    }
  }

  :global(.mx-auto) {
    margin-left: auto;
    margin-right: auto;
  }

  :global(.w-full) {
    width: 100%;
  }

  :global(.last\:border-b-0:last-child) {
    border-bottom-width: 0px;
  }
</style> 