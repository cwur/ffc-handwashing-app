<script>
  import ProgressBar from "./ProgressBar.svelte";

  let initialSeconds = 20;
  let secondsLeft = initialSeconds;
  $: progress = (initialSeconds -  secondsLeft) / initialSeconds * 100;

  let timerRunning = false;
  const startTimer = () => {
    timerRunning = true;
    const timer = setInterval(() => {
        secondsLeft -= 1;
        if (secondsLeft === 0) {
            clearInterval(timer);
            timerRunning = false;
            secondsLeft = initialSeconds;
        }
    }, 1000);
  }
</script>

<style>
  .start {
    background-color: rgb(124, 28, 28);
    width: 100%;
    margin: 10px 0;
  }
  .start[disabled] {
      filter: grayscale(50%);
      cursor: not-allowed;
  }
</style>

<div bp="grid">
  <h2 bp="offset-5@md 4@md 12@sm">Seconds Left: {secondsLeft}</h2>
</div>

<ProgressBar progress={progress}/>

<div bp="grid">
    <button 
        bp="offset-5@md 4@md 12@sm" 
        disabled={timerRunning}
        class="start" 
        on:click|once={startTimer}
    >
        Start
    </button>
</div>
