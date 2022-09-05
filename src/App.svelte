<script>
  import { intervalToDuration } from 'date-fns';
  import Bat from './lib/Bat.svelte';
  import Confetti from './lib/Confetti.svelte';

  const birthTime = new Date('2/5/22, 22:30');
  let age;
  let showConfetti = false;

  const getDiff = () => {
    const { years, months, days, hours, minutes, seconds } = intervalToDuration({
      start: birthTime,
      end: new Date(),
    });
    // if (seconds < 5 && minutes === 0 && hours === 0 && days === 0 && years < 1) {
    //   showConfetti = true;
    // } else {
    //  showConfetti = false;
    // }

  if (seconds < 5 &&) {
    showConfetti = true
  } else { 
    showConfetti = false
  }

    age = `${years} år ${months} månader ${days} dagar ${hours} timmar ${minutes} minuter`;
  };

  setInterval(getDiff, 200);
</script>

<svelte:head>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" />
  <link
    href="https://fonts.googleapis.com/css2?family=Shadows+Into+Light&display=swap"
    rel="stylesheet"
  />
</svelte:head>

<main>
  {#if showConfetti}
    <div class="confetti">
      <Confetti />
    </div>
  {/if}
  <div class="content">
    <h1>
      OZZY{' '}
      <span> VALENTIN LARS-OVE </span>{' '}
      VESTBERG
    </h1>
    <h3>
      {' '}
      05/02-22 • 3244G • 50CM
    </h3>
    <h3>
      {age}
    </h3>
  </div>
  <div class="bat">
    <Bat />
  </div>
</main>

<style>
  main {
    height: 100vh;
    width: 100vw;
    background: #0e1116;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  h1 {
    font-size: 3em;
    padding: 0 16px;
    font-family: sans-serif;
    text-align: center;
    color: rgb(202, 209, 216);
  }

  h3 {
    font-family: 'Shadows Into Light';
    padding: 8px 16px;
    color: rgb(202, 209, 216);
    font-size: 1.8em;
    text-align: center;
  }

  span {
    color: rgb(202, 209, 216, 0.1);
  }

  .content {
    position: relative;
    height: 100vh;
    top: 0;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    z-index: 999;
  }

  .bat {
    position: absolute;
    width: 100vw;
    top: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1;
  }

  .confetti {
    position: fixed;
    top: -50px;
    left: 0;
    height: 100vh;
    width: 100vw;
    display: flex;
    justify-content: center;
    overflow: hidden;
    pointer-events: none;
  }

  @media (min-width: 1024px) {
    h1 {
      font-size: 5em;
    }

    h3 {
      font-size: 3em;
    }
  }
</style>
