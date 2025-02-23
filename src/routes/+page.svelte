<script>
	import {user} from '../stores/user';
  import Typewriter from 'svelte-typewriter';
  import LogInForm from '../components/LogInForm.svelte';
  import AxiomPreamble from '../components/axioms/AxiomPreamble.svelte';
  import Navigation from '../components/Navigation.svelte';
  import Decrypting from '../components/Decrypting.svelte';
  import AxiomControls from '../components/axioms/AxiomControls.svelte';
  import Axiom1-6 from '../components/axioms/Axiom1-6.svelte';
  import Axiom7-11 from '../components/axioms/Axiom7-11.svelte';
  import Axiom12-18 from '../components/axioms/Axiom12-18.svelte';
  import Axiom19-24 from '../components/axioms/Axiom19-24.svelte';
  import Axiom25-31 from '../components/axioms/Axiom25-31.svelte';
  import Axiom32-37 from '../components/axioms/Axiom32-37.svelte';
  import Preparations from '../components/Preparations.svelte';
  import AxiomsIntro from '../components/axioms/AxiomsIntro.svelte';

  let showLogin = false,
    showTypedHeader = true,
    loggedIn = false,
    loading = false,
    navigationOpen = false,
    axiomPreambleOpen = false,
    axiomReadBtnAvailable = false,
    PreparationsReadBtnAvailable = false,
    axiomsOpen = false,
    axiom = 1,
    showAxioms = false,
    showPreparations = false,
    PreparationsOpen = false;

  const jumpToNavigation = () => {
    if (loading) loading = false;
    if (axiomPreambleOpen) axiomPreambleOpen = false;
    if (axiomReadBtnAvailable) axiomReadBtnAvailable = false;
    if (PreparationsReadBtnAvailable) PreparationsReadBtnAvailable = false;
    if (axiomsOpen) axiomsOpen = false;
    if (showAxioms) showAxioms = false;
    if (showPreparations) showPreparations = false;
    if (PreparationsOpen) PreparationsOpen = false;
    axiom = 1;
    navigationOpen = true;
  }

  const lastAxiom = () => {
    if (axiom === 1) {
      axiom = 7;
    } else {
      axiom = axiom - 1;
    }
  };

  const nextAxiom = () => {
    if (axiom === 7) {
      axiom = 1;
    } else {
      axiom = axiom + 1;
    }
  };
</script>

<svelte:head>
	<title>Secure Server v24.8 </title>
	<meta name="description" content="Scientia Mors Est" />
</svelte:head>

<div class="mt-14 w-9/12 lg:w-3/5 xl:w-2/5 flex flex-col items-center">
{#if loggedIn === false}
  <Typewriter interval={47} on:done={() => showLogin = true}>
    <h1 class="text-3xl">Welcome to the <span class="text-5xl text-delta-green">Δ</span> Secure Server v24.8</h1>
  </Typewriter>

  {#if showLogin} <!-- Triggers once the welcome message is completed -->
    <div class="md:w-3/4 lg:w-2/4 xl:w-2/5">
      <LogInForm bind:loggedIn={loggedIn} />
    </div>
  {/if}
{:else}
  {#if showTypedHeader}
    <Typewriter interval={47} on:done={() => {loading = true; showTypedHeader = false;}}>
      <h1 class="text-3xl mb-5"> Welcome <span class="text-delta-green times24">{$user}</span> to the
        <span class="text-5xl text-delta-green cursor-pointer">Δ</span>
        Secure Server
      </h1>
    </Typewriter>
  {:else}
    <h1 class="text-3xl mb-5"> Welcome <span class="text-delta-green times32">{$user}</span> to the
      <button class="text-5xl text-delta-green cursor-pointer" on:click={jumpToNavigation}>Δ</button>
      Secure Server
    </h1>
  {/if}

  {#if loading}
    <Decrypting onFinish={() => setTimeout(() => { loading = false; navigationOpen = true }, 380)} />
  {/if}

  {#if navigationOpen}
    <Navigation
      correspondenceFn={() => { axiomPreambleOpen = true; navigationOpen = false }}
    />
  {/if}

  {#if axiomPreambleOpen}
    <AxiomPreamble onFinish={() => {axiomReadBtnAvailable = true; PreparationsReadBtnAvailable = true}} />

    {#if axiomReadBtnAvailable}
      <button
        type="button"
        class="rounded bg-slate-700 text-xl p-2 border border-blue-300 border-opacity-25 hover:border-delta-green mb-4"
          on:click={() => {axiomPreambleOpen = false; axiomsOpen = true; showPreparations = false;}}
        >
        Open Attachment
        <span class="text-md text-gray-400">(Axioms.txt)</span>
      </button>
  {/if}
      
    {#if PreparationsReadBtnAvailable}
      <button
        type="button"
        class="rounded bg-slate-700 text-xl p-2 border border-blue-300 border-opacity-25 hover:border-delta-green mb-4"
          on:click={() => { axiomPreambleOpen = false; PreparationsOpen = true; showAxioms = false;}}
        >
        Open Attachment
        <span class="text-md text-gray-400">(Preparations.txt)</span>
      </button>  
    {/if}
  {/if}

  {#if axiomsOpen} <!-- Triggers when they first open the axioms attachment -->
    <Typewriter cascade on:done={() => {showAxioms = true}}>
      <span class="text-delta-green text-lg"> ALPHONSE'S AXIOMS FOR AGENTS </span>
    </Typewriter>

    {#if showAxioms} <!-- Triggers after the title is displayed -->
      {#if axiom === 1} <AxiomsIntro /> {/if}
      {#if axiom === 2} <Axiom1-6 /> {/if}
      {#if axiom === 3} <Axiom7-11 /> {/if}
      {#if axiom === 4} <Axiom12-18 /> {/if}
      {#if axiom === 5} <Axiom19-24 /> {/if}
      {#if axiom === 6} <Axiom25-31 /> {/if}
      {#if axiom === 7} <Axiom32-37 /> {/if}

      <AxiomControls lastFn={lastAxiom} nextFn={nextAxiom} />
    {/if}
  {/if}<!-- Not Logged in -->

  {#if PreparationsOpen} <!-- Triggers when they first open the Preparations attachment -->
      <Typewriter cascade on:done={() => { showPreparations = true; }}>
        <span class="text-delta-green text-lg"> PREPARATIONS FOR OPERATIVES </span>
      </Typewriter>

      {#if showPreparations}
        <Preparations />
      {/if}
    {/if}
  {/if}
</div>
