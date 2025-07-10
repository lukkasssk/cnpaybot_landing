<script>
  import Hero from './Hero.svelte'
  import HowItWorks from './HowItWorks.svelte'
</script>

<div class="hero-phone-section">
  <div class="content-left">
    <Hero />
  </div>
  <div class="content-right">
    <HowItWorks />
  </div>
</div>

<style>
  .hero-phone-section {
    padding: 6rem 2rem;
    display: flex;
    margin-top: 5rem;
    padding-bottom: 1rem;
    width: 100%;
    justify-content: center;
    align-items: center;
    max-width: 1400px;
    margin-left: auto;
    margin-right: auto;
  }

  .content-left {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    max-width: 50%;
    padding: 0 1rem;
  }

  .content-right {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    max-width: 50%;
    padding: 0 1rem;
  }

  @media (max-width: 768px) {
    .hero-phone-section {
      flex-direction: column;
      padding: 3rem 1rem;
    }
    
    .content-left,
    .content-right {
      width: 100%;
      max-width: 100%;
      padding: 0;
    }
  }
</style> 