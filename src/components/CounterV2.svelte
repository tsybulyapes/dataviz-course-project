<script>
  import { onMount, onDestroy } from 'svelte'
  

  export let start = 0
  export let end = 3000000000
  export let duration = 8000 // in milliseconds
  export let text = 'in cash and assets involved'
  let count = start
  let interval
  let step
  let mounted = false
  

  const updateCount = () => {
    step = (end - start) / (duration / 50) // Calculate step based on duration
    interval = setInterval(() => {
      count += step
      if ((step > 0 && count >= end) || (step < 0 && count <= end)) {
        count = end
        clearInterval(interval)
      }
    }, 50)
  }

  onMount(() => {
    mounted = true
    updateCount()
  })

  onDestroy(() => {
    clearInterval(interval)
  })
</script>

<div class="counter">
  {#if mounted}
    

    <div class="value">
      <p>${Math.round(count).toLocaleString('en-US')}</p>
    </div>
    <p class="text-opening">{text}</p>
  {/if}
</div>

<style>
  .counter {
    width: 100%;
    height: 170px;
    max-width: 43.75rem;
    margin: 50px auto 30px auto;
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: center;
    color: #fff
  }
  .pict {
      width: 160px;
      margin-bottom: 10px;
    }
    .value {
      border: solid 2px #fff;
      width: fit-content;
      padding: 5px 20px;
      margin-bottom: 10px;
      border-radius: 15px;
      min-width: 330px;
      
    }
    p {
        font-size: 40px;
        margin: 0;
      }
</style>
