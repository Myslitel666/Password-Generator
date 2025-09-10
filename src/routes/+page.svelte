<script lang="ts">
  import { themeStore } from "svelte-elegant/stores";
  import { onMount, onDestroy } from "svelte";
  import { Button, Checkbox, TextField } from "svelte-elegant";

  let length = "10";

  let isInitialized = false;
  let isUseNumbers = true;
  let isUseLowercase = true;
  let isUseUppercase = true;
  let isUseSymbols = true;

  onMount(() => {
    isInitialized = true;
  });
</script>

<div class="page">
  <div class="option" style:margin-top="10px">
    <p style:margin-right="7px">Enter the password length:</p>
    <TextField
      type="number"
      label="Length"
      width="145px"
      bind:value={length}
      textAlign="right"
    />
  </div>
  <div>
    <div class="option">
      <Checkbox bind:isActive={isUseNumbers} />
      <p style:margin-left="4px">Use Numbers</p>
    </div>
    <div class="option">
      <Checkbox bind:isActive={isUseLowercase} />
      <p style:margin-left="4px">Use Lowercase (a-z)</p>
    </div>
    <div class="option">
      <Checkbox bind:isActive={isUseUppercase} />
      <p style:margin-left="4px">Use Uppercase (A-Z)</p>
    </div>
    <div class="option">
      <Checkbox bind:isActive={isUseSymbols} />
      <p style:margin-left="4px">Use Symbols</p>
    </div>
  </div>
  <Button marginTop="3px">Generate Password</Button>
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
