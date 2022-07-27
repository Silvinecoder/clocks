<script>
  let clockElement;
  let secondsHand;
  let minsHand;
  let hourHand;

  let seconds = 0; 
  setInterval(() => {
    seconds++; 

    if (seconds > 0.1) {
      clearInterval();
      clock();
    }
  }, 1000);

  function clock() {
    clockElement.style.cssText = 'visibility: visible; opacity: 1;';

    function setDate() {
      const now = new Date();

      function time() {
        const seconds = now.getSeconds(); 
        const secondsDegrees = (seconds / 60) * 360 + 90;
        secondsHand.style.transform = `rotate(${secondsDegrees}deg)`;

        const mins = now.getMinutes(); 
        const minsDegrees = (mins / 60) * 360 + (seconds / 60) * 6 + 90;
        minsHand.style.transform = `rotate(${minsDegrees}deg)`;

        
        const hour = now.getHours(); 
        const hourDegrees = (hour / 12) * 360 + (mins / 60) * 30 + 90;
        hourHand.style.transform = `rotate(${hourDegrees}deg)`;
      }

      time();
    }

    setDate();
    console.log(setDate);
  }
</script>


<div class="clock" bind:this={clockElement}>

  <div class="outer-clock-face">
    <div class="marking marking-one" />
    <div class="marking marking-two" />
    <div class="marking marking-three" />
    <div class="marking marking-four" />


    <div class="inner-clock-face">
      <div class="hand hour-hand" bind:this={hourHand} />
      <div class="hand min-hand" bind:this={minsHand} />
      <div class="hand second-hand" bind:this={secondsHand} />
    </div>
  </div>
</div>

<style lang="scss">
  .clock {
    border: 4px solid #ffff;
    border-radius: 50%;
    height: 80px;
    visibility: hidden;
    opacity: 0;
    transition: visible 0s, opacity 0.3s linear;
    width: 80px;



    .outer-clock-face {
      background: #222831;
      border-radius: 100%;
      height: 100%;
      position: relative;
      width: 100%;

      &::after {
        transform: rotate(90deg);
      }

      &::after,
      &::before,
      .marking {
        background: #08d9d6;
        content: '';
        left: 50%;
        height: 100%;
        position: absolute;
        width: 2px;
        z-index: 0;
      }


      .marking {
        background: #eeeeee;
        width: 2px;
      }

      .marking-one {
        transform: rotate(30deg);
      }

      .marking-two {
        transform: rotate(60deg);
      }

      .marking-three {
        transform: rotate(120deg);
      }

      .marking-four {
        transform: rotate(150deg);
      }
    }

    .inner-clock-face {

      background: #222831;
      border-radius: 100%;
      height: 80%;
      left: 11%;
      position: absolute;
      top: 10%;
      width: 80%;
      z-index: 1;

      .hand {
        border-radius: 6px;
        height: 4px;
        position: absolute;
        right: 50%;
        transform-origin: 100%;
        transform: rotate(90deg);
        transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1);
        top: 50%;
        width: 40%;
      }

      .hour-hand {
        background: #3f72af;
        width: 26%;
        z-index: 2;
      }

      .min-hand {
        background: #08d9d6;
        height: 3px;
        width: 40%;
        z-index: 1;
      }

      .second-hand {
        background: #ff2e63;
        height: 2px;
        width: 50%;
      }
    }
  }
</style>
