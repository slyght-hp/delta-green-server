<script type="ts">
  import Typewriter from 'svelte-typewriter';
  import LoopDecode from '../effects/LoopDecode.svelte';

  let showFrom = false
</script>

<Typewriter cascade interval={20} on:done={() => showFrom = true}>
  <br />
  <ol>
    <li>
      <p><span class="text-delta-green">31. When you don't have enough force to assault the opposition's stronghold, burn it.</span></p>
      <p class="pl-6 mb-4">  Flush them out and ambush their escape route. </p>
    </li>
      <p><span class="text-delta-green">32. You're safer if you never get out of range of encrypted radio with your teammates.</span></p>
      <p class="pl-6 mb-4">  You're safest if you never get out of each others' sight. </p>
    </li>
      <p><span class="text-delta-green">33. Use old cars.</span></p>
      <p class="pl-6">  No Lojack, no airbags, no automatic locks. </p>
      <p class="pl-6 mb-4">  Manual everything, if you can get it. </p>
    </li>
      <p><span class="text-delta-green">34. Never bring anything to the Opera if you can't drop it and walk away.</span></p>
      <p class="pl-6">  Never bring anything you didn't buy with cash. </p>
      <p class="pl-6">  Never, ever bring anything your home agency issued to you. </p>
      <p class="pl-6 mb-4">  Ever. </p>
    </li>
      <p class="mb-4"><span class="text-delta-green">35. Do not fuck with magic.</span></p>
    </li>
      <p class="mb-4"><span class="text-delta-green">36. Never leave teammates behind, or where the authorities can find them.</span></p>
    </li>
      <p class="mb-4"><span class="text-delta-green">37. Always report back to your handler.
  </ol>
  <br />
  <br />
</Typewriter>

{#if showFrom}
--<LoopDecode />
{/if}
