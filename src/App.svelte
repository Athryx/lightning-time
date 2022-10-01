<script lang="ts">
  let timeString = "0~0~0~0";
  let milliSparks = 0;
  let sparks = 0;
  let zaps = 0;
  let bolts = 0;

  const millisPerMilliSpark = 1318.359375;

  function updateTime() {
    const time = new Date();
    const millis = 1000 * 60 * 60 * time.getHours() + 1000 * 60 * time.getMinutes() + 1000 * time.getSeconds() + time.getMilliseconds();
    const totalMilliSparks = millis / millisPerMilliSpark;
    const totalSparks = totalMilliSparks / 16;
    const totalZaps = totalSparks / 16;
    const totalBolts = totalZaps / 16;

    milliSparks = Math.floor(totalMilliSparks) % 16;
    sparks = Math.floor(totalSparks) % 16;
    zaps = Math.floor(totalZaps) % 16;
    bolts = Math.floor(totalBolts) % 16;

    timeString = bolts.toString(16) + "~" + zaps.toString(16) + "~" + sparks.toString(16) + "|" + milliSparks.toString(16);
  }

  updateTime();
  setInterval(updateTime, 100);
</script>

<div style:background-image={`linear-gradient(90deg, rgb(${bolts * 16 + zaps}, 161, 0), rgb(150, ${zaps * 16 + sparks}, 100), rgb(85, 66, ${sparks * 16 + milliSparks}))`}>
  <h1>{timeString}</h1>
</div>

<style>
  div {
    width: 100%;
    height: 1100px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  h1 {
    font-size: 5rem;
    line-height: 1.1;
  }
</style>