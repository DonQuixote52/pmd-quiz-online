<script>
  import { onMount } from "svelte";
  export let musicBg = null;
  let volume = 10;
  let showVolumeSlider = false;

  onMount(() => {
    if (musicBg) {
      musicBg.volume = volume / 100;
    }
  });

  function toggleVolumeSlider() {
    showVolumeSlider = !showVolumeSlider;
  }

  function handleVolumeChange(event) {
    volume = event.target.value;
    if (musicBg) {
      musicBg.volume = volume / 100;
    }
  }
</script>

<button on:click="{toggleVolumeSlider}" class="volume-button backdrop-blur-lg">
  Volume
</button>

{#if showVolumeSlider}
  <div class="volume-slider-container">
    <input
      type="range"
      min="0"
      max="100"
      value="{volume}"
      on:input="{handleVolumeChange}"
      class="volume-slider" />
  </div>
{/if}

<style>
  .volume-button {
    position: absolute;
    top: 1rem;
    right: 1rem;
    padding: 0rem 0.5rem;
    text-align: center;
    color: white;
    background-color: hsla(300, 2%, 13%, 0.75);
    border-radius: 15px;
    border: 15px solid transparent;
    border-image: url(/img/others/pmdtextbox.png) 43 round;
    cursor: pointer;
    z-index: 100;
  }

  .volume-slider-container {
    position: absolute;
    top: 1rem;
    right: 1rem;
    transform: translateX(-50%);
    background-color: rgba(0, 0, 0, 0.8);
    padding: 0.75rem;
    border-radius: 0.5rem;
    z-index: 99;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .volume-slider {
    width: 10rem;
  }

  @media (max-width: 600px) {
    .volume-button {
      top: 0.5rem;
      right: 0.5rem;
      padding: 0.25rem 0.5rem;
    }

    .volume-slider-container {
      top: 0.5rem;
      right: 0.5rem;
      padding: 0.4rem;
    }

    .volume-slider {
      width: 8rem;
    }
  }
</style>
