	
<script lang="ts">
    import { onMount } from "svelte";
    import { Progress } from "$lib/components/ui/progress/index.js";
   
    let rewardValue = $state(13);
    let currentValue = $state(13);
   
    onMount(() => {
      const timer = setTimeout(() => {rewardValue = 66; currentValue = 100}, 500);
      return () => clearTimeout(timer);
    });
</script>
   
<div class="flex flex-col items-center justify-center w-full gap-y-2">
    <h1>Next reward</h1>
    <Progress value={rewardValue} max={100} class="w-[60%]" />
    <h1>Current</h1>
    <Progress value={currentValue} max={100} class="w-[60%]" />
</div>