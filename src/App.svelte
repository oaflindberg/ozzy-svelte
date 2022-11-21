<script>
  import { intervalToDuration } from 'date-fns';
  import Bat from './lib/Bat.svelte';
  import Confetti from './lib/Confetti.svelte';

  const birthTime = new Date('2/5/22, 22:30');
  let age;
  let yearsAge;
  let monthsAge;
  let daysAge;
  let hoursAge;
  let minutesAge;
  let secondsAge;
  let showConfetti = false;

  const getDiff = () => {
    const { years, months, days, hours, minutes, seconds } = intervalToDuration({
      start: birthTime,
      end: new Date(),
    });

    if (seconds < 5) {
      if (years >= 1 && months === 0 && days === 0 && hours === 0 && minutes === 0) {
        showConfetti = true;
      } else if (years < 1 && days === 0 && hours === 0 && minutes === 0) {
        showConfetti = true;
      } else {
        showConfetti = false;
      }
    } else {
      showConfetti = false;
    }

    yearsAge = `${years} år`;
    monthsAge = `${months} ${months === 1 ? 'månad' : 'månader'}`;
    daysAge = `${days} ${days === 1 ? 'dag' : 'dagar'}`;
    hoursAge = `${hours} ${hours === 1 ? 'timme' : 'timmar'}`;
    minutesAge = `${minutes} ${minutes === 1 ? 'minut' : 'minuter'}`;
    secondsAge = `${seconds} ${seconds === 1 ? 'sekund' : 'sekunder'}`;
    age = `${yearsAge} ${monthsAge} ${daysAge} ${hoursAge} ${minutesAge} ${secondsAge}`;
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
    <h3 class="info">
      {' '}
      05/02-22 • 3244G • 50CM
    </h3>
    <div class="age">
      <h3 class="age-desktop">
        {age ?? 'Räknar ut ålder'}
      </h3>
      {#if !age}
        <h3>Räknar ut ålder</h3>
      {:else}
        <h3 class="age-mobile">
          {`${yearsAge} ${monthsAge}`}
        </h3>
        <h3 class="age-mobile">
          {`${daysAge} ${hoursAge}`}
        </h3>
        <h3 class="age-mobile">
          {minutesAge}
        </h3>
        <h3 class="age-mobile">
          {secondsAge}
        </h3>
      {/if}
    </div>
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
    font-family: Helvetica, sans-serif;
    text-align: center;
    color: rgb(202, 209, 216);
    height: 200px;
    margin: 0 auto;
  }

  .info {
    padding: 60px 0 20px 0;
  }

  .age {
    width: 260px;
    height: 200px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .age-mobile {
    padding: 0;
  }

  .age-desktop {
    display: none;
  }

  h3 {
    font-family: 'Shadows Into Light';
    padding: 0px 16px;
    color: rgb(202, 209, 216);
    font-size: 1.8em;
    text-align: center;
  }

  span {
    -webkit-text-stroke-width: 1px;
    -webkit-text-stroke-color: rgba(202, 209, 216, 0.3);
    color: transparent;
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

    .age {
      width: 100%;
    }

    .age-desktop {
      display: flex;
    }

    .age-mobile {
      display: none;
    }

    h3 {
      font-size: 3em;
    }
  }
</style>
