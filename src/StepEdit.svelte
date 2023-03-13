<script lang="ts">
  import "two-up-element";
  import { originalImage, modifiedImage } from "./store";

  let processingImage = true;
  let tries = 0;
  let intervalId: any;

  $: {
    if (processingImage) {
      clearInterval(intervalId);
      intervalId = setInterval(() => {
        tries++;
        const img = new Image();
        img.src = $modifiedImage;
        img.onload = () => {
          processingImage = false;
          clearInterval(intervalId);
        };
      }, 500);
    }
  }
</script>

{#if processingImage}
  <div class="flex flex-col justify-center items-center">
    <div class="lds-ripple">
      <div />
      <div />
    </div>
    <p class="text-center mt-4">Prosesando Imagen ...</p>
  </div>
{:else}
  <two-up>
    <img src={$originalImage} alt="Imagen original subida por el usuario" />
    <img src={$modifiedImage} alt="Imagen sin fondo subida por el usuario" />
  </two-up>
  <a
    download
    href={$modifiedImage}
    class="block bg-blue-500 hover:bg-blue-700 w-full text-center font-bold text-white rounded-full px-4 py-2 mt-10"
    >Descargar Imagen sin fondo</a
  >
{/if}
