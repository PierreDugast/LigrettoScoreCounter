<script>
	import { fade } from 'svelte/transition';
	import { storeFE } from './store.js';
	export let objAttributes = {};
	
	function removeComponent() {
		$storeFE = $storeFE.filter(function(value, index, arr){ 
			if (value.id != objAttributes.id) return value;
		});
		console.log($storeFE);
	}
</script>
<li transition:fade>
	<!-- {objAttributes.name} (id={objAttributes.id})  -->
	<!-- {#if objAttributes.otherattrib}<em>{objAttributes.otherattrib}</em>{/if}
	<button on:click={removeComponent}>x</button> -->
    
    <div class="w-screen max-w-sm md:max-w-lg rounded-lg shadow-lg p-4 mt-10 bg-white ">
        <div class="Card"rank></div>
        <h3 class="font-semibold text-lg text-gray-700 tracking-wide">{objAttributes.name}</h3>
        <p class="text-black-700 my-1">
            score : 
       </p>
        <p class="text-gray-500 my-1">
            history
        </p>
</li>