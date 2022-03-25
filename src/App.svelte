<script>
    import { selections } from './data.js';
    import { onMount } from 'svelte'

    let key;
    let item = selections[Math.floor(Math.random()*selections.length)];
    let firstTime = true;
    let activated = false;

    $: color = item.color;
    $: isImage = item.isImage;
    $: path = item.path;


    function handleEvent(event) {
        if (firstTime) {
            const audio = new Audio();
            audio.src = "audio/bird.mp3";
            audio.play();

            firstTime = false;
        }
        item = selections[Math.floor(Math.random()*selections.length)];
        activated = true;
    }

</script>

<svelte:window on:keydown={handleEvent} on:click={handleEvent}/>

<main>
    {#if activated}
        <div >
            {#if isImage}
                <img src={path} alt='slaughterhouse 5'/>
            {:else}
                <embed src={path} width="538" height="540">
            {/if}
        </div>
    {:else}
        <h1>Press any key to begin</h1>
    {/if}
</main>

<style lang="postcss" global>
  @tailwind base;
  @tailwind components;
  @tailwind utilities;

  main {
      position: absolute;
      width:100vw;
      height:100vh;
      display:flex;
      justify-content:center;
      align-items:center;

      animation: background-fade 10s infinite;
  }
  @keyframes background-fade {
      0% {
          background-color: #3B78D8;
      }
      33% {
          background-color: #E59138;
      }
      66% {
          background-color: #F1C231;
      }
      100% {
          background-color: #664EA7;
      }
  }
</style>

