<script lang="ts">
  import { themeStore } from "svelte-elegant/stores";
  import { onMount, onDestroy } from "svelte";
  import { ButtonBox, Checkbox, TextField } from "svelte-elegant";
  import { Play, Pause } from "svelte-elegant/icons-elegant";

  let isInitialized = false;
  let isStopped = true;
  let rememberedTime = 0;
  let elapsedTime = 0;
  const timeStartConst = "00";
  let minutes = timeStartConst;
  let seconds = timeStartConst;
  let ms = timeStartConst;
  let timerInterval: number | null = null;

  function formatTimeUnits(value: number) {
    return (value % 60).toString().padStart(2, "0");
  }

  function initialTimer() {
    const startTime = Date.now();

    timerInterval = setInterval(() => {
      elapsedTime = rememberedTime + Date.now() - startTime;

      minutes = formatTimeUnits(Math.floor(elapsedTime / 60000));
      seconds = formatTimeUnits(Math.floor(elapsedTime / 1000));
      ms = formatTimeUnits(Math.floor(elapsedTime / 16.666));
    }, 60); // Интервал не важен, можно 16ms (~60fps)
  }

  function clearTimer() {
    if (timerInterval) {
      clearInterval(timerInterval);
      timerInterval = null;
    }
  }

  onMount(() => {
    isInitialized = true;
  });

  // ОЧИЩАЕМ ТАЙМЕР ПРИ УНИЧТОЖЕНИИ КОМПОНЕНТА
  onDestroy(() => {
    if (timerInterval) {
      clearInterval(timerInterval);
      timerInterval = null;
    }
  });
</script>

<div class="page">
  <div class="option" style:margin-top="10px">
    <p style:margin-right="4px">Enter the password length:</p>
    <TextField type="number" label="Length" width="145px" textAlign="right" />
  </div>
  <div>
    <div class="option">
      <Checkbox />
      <p style:margin-left="4px">Use Numbers</p>
    </div>
    <div class="option">
      <Checkbox />
      <p style:margin-left="4px">Use Lowercase (a-z)</p>
    </div>
    <div class="option">
      <Checkbox />
      <p style:margin-left="4px">Use Uppercase (A-Z)</p>
    </div>
    <div class="option">
      <Checkbox />
      <p style:margin-left="4px">Use Symbols</p>
    </div>
  </div>
</div>

<style>
  .option {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
  }

  .page {
    width: 100vw;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  .timer {
    font-size: 48px;
    margin-top: 30px;
    margin-bottom: 30px;
  }

  .ms {
    font-size: 20px;
    margin-left: 5px;
  }
</style>
