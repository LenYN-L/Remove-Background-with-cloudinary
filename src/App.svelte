<script lang="ts">
  import { ImageStatus } from "../types.d";
  import CloudinaryLogo from "./CloudinaryLogo.svelte";
  import StepEdit from "./StepEdit.svelte";
  import StepUpload from "./StepUpload.svelte";
  import { imageStatus } from "./store";
</script>

<div
  class="bg-slate-300 h-screen"
>
  <header class="flex justify-center py-10">
    <h1 class="text-3xl font-bold text-blue-900 tracking-tighter">
      remove<span class="text-blue-600">bg</span>
    </h1>
  </header>
  <main class="max-w-xl mx-auto border-dotted border-black border-4">  
    {#if $imageStatus === ImageStatus.READY || $imageStatus === ImageStatus.UPLOADING}
      <StepUpload />
    {:else if $imageStatus === ImageStatus.DONE}
      <StepEdit />
    {/if}
  </main>

  <footer class="flex justify-center gap-x-2 font-semibold pt-10">
    Hecho con <CloudinaryLogo />
  </footer>
</div>
