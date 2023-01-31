<script>
  import { SyncLoader } from 'svelte-loading-spinners'
  import { fly } from 'svelte/transition'

  export let src
  export let alt

  const lazyLoading = function () {
    return new Promise((resolve) => {
      const img = new Image()
      img.onload = resolve
      img.src = src
    })
  }
</script>

{#await lazyLoading()}
  <div class="flex justify-center w-full">
    <SyncLoader size="100" color="#2dd4bf" unit="px" duration="1s" />
  </div>
{:then data}
  <img {src} {alt} in:fly={{ duration: 500, opacity: 1, x: -400 }} />
{/await}
