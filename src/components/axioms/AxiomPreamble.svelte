<script type="ts">
  import Typewriter from 'svelte-typewriter';
  export let onFinish;
</script>

<Typewriter cascade on:done={onFinish}>
  <p class="text-center pb-4"> Something is wrong in Hellbend, California. </p>

  <p class="text-center"> Two civilians have been murdered. </p>

  <p class="text-center"> Their bodies were torn apart. </p>

  <p class="text-center pb-4"> It's up to you to find out why. </p>

  <ul class="flex flex-col items-center pb-4">
    <li class="text-center w-full">Agent, your mission is as follows: </li>
    <li class="self-start">1) Determine who or what is killing the people of Hellbend.</li>
    <li class="self-start">2) If the threat is unnatural, isolate it and destroy it.</li>
    <li class="self-start">3) Close the case so law enforcement doesn't look any closer.</li>
    <li class="self-start">4) 4) Leave no witnesses to any unnatural events.</li>
  </ul>
	
  <p class="text-center"> Time is of the essence. </p>

  <p class="text-center"> You will find further details in the attached files. </p>

</Typewriter>
