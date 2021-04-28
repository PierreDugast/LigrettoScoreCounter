<script>

  import PlayerCard from "./PlayerCard.svelte";
  import Header from "./Header.svelte";
  import Footer from "./Footer.svelte";
  import { flip } from "svelte/animate";
  import { fly,fade } from 'svelte/transition';

 


  import { storeFE, idIncrement } from './store.js';

  import { beforeUpdate, afterUpdate } from 'svelte';

	let div;
	let autoscroll;

	beforeUpdate(() => {
		autoscroll = div && (div.offsetHeight + div.scrollTop) > (div.scrollHeight - 20);
	});

	afterUpdate(() => {
		if (autoscroll) div.scrollTo(0, div.scrollHeight);
	});



  $storeFE = [
		// { id:0, name: 'Pierre', score: 3,history: '4-5+4', rank:1 },
		// other items can go here
	];

	idIncrement.set(0);	// this is a crude way to increment the id for new items




  function handleAddPlayer(){
	var l = $storeFE.length;	// get our current items list count
		$storeFE[l] = { id:$idIncrement, name: '', score: '',history: '', rank: '' };
		// console.log($storeFE);
		$idIncrement++;	// increment our id to add additional items
  }

  
  function reset(){
		storeFE.set([]);
		idIncrement.set(0);	// increment our id to add additional items
  }


  $:sorted=$storeFE.sort((a,b)=>b.score - a.score);

</script>


<!-- Éléments page -->
<div class="flex flex-col h-screen">
	<Header on:click={reset} />
	<main class="flex flex-grow justify-center">
		<ul bind:this={div}>
			{#each sorted as item,index (item)}
				<div animate:flip={{ duration: 300 }} out=fade>
					<svelte:component this={PlayerCard} objAttributes={item} rank2  ={index+1} />
				</div>
			{/each}
		</ul>
	</main>
	<Footer on:click={handleAddPlayer}/>
</div>


<style global>
	@tailwind base;
	@tailwind components;
	@tailwind utilities;

	body{
        background-color:  #f9fafb ;
    }

	ul{ 
		margin-bottom:80px;
	}


</style>
