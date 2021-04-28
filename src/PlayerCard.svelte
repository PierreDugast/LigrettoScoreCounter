<script>
    import { storeFE } from './store.js';
    import { fly,fade } from 'svelte/transition';


    
    export let objAttributes = {};
    export let rank2;

    let win;


    objAttributes.score = parse(objAttributes.history);

    function removeComponent() {
		$storeFE = $storeFE.filter(function(value, index, arr){ 
			if (value.id != objAttributes.id) return value;
		});
		console.log($storeFE);
	}

    function yell() {
		console.log("name updated");

	}

    function parse(str) {
        if (str.length != 0){
            return Function(`'use strict'; return (${str})`)()
            } else{
                return '';
            }
    }


    

    function updateHistory() {
        objAttributes.score = parse(objAttributes.history);

        //Màj ordre affichage

        if (objAttributes.score == 100){
            win = true;
        }else{
            win = false;
        }
        $storeFE = $storeFE;

	}

   

</script>

<!-- in:fly="{{ y: 200, duration: 500 }}" out:fly -->

    <li  in:fly="{{ y: 200, duration: 500 }}" out:fly="{{ y: 200, duration: 500 }}">
            <div class="{win ? 'w-screen max-w-sm md:max-w-lg rounded-lg shadow-lg p-4 mt-10 bg-green-300' : 'w-screen max-w-sm md:max-w-lg rounded-lg shadow-lg p-4 mt-10 bg-white'}">
                <div class="Card"><p class="test">{rank2}</p></div>
                {#if win}
                    <div class="crown font-bold text-xl text-gray-700 transform rotate-35 shadow-2xl ">👑</div>
                {/if}
                <button class='delete h-8 py-1 px-3 text-s font-semibold rounded-full hover:bg-red-500 text-white focus:outline-none focus:ring-2 focus:ring-blue bg-gray-600 z-10' on:click={removeComponent} >X</button>
                <h3 class="name font-bold text-xl text-gray-900 "><input class="pr-4 pl-4 pt-4 pb-4 rounded-lg shadow-inner bg-gray-100"placeholder="Joueur" on:input={yell} bind:value={objAttributes.name} ></h3>
                <div class="score text-black-700 text-l font-semibold rounded-full ml-60">
                    <p>Score {#if objAttributes.score.length != 0}  <span class="text-black-700 text-l font-semibold rounded-full bg-gray-200 pt-1 pb-1 pr-2 pl-2 ">{objAttributes.score}</span>{/if}</p>
                </div>
                <p class="text-gray-500 my-1 ">
                    <input class="hist_input shadow-inner" type=text placeholder="" on:input={updateHistory} bind:value={objAttributes.history} >
                </p>
            
            </div>
        
    </li> 
    




<style>
    .score {
        display:block;
        text-align: center;
        max-width: 50px;
    }
            
    .crown {
        width: 24px;
        position :relative;
        left:95%;
        top:-90px;
        --tw-rotate: 35deg;
    }

    
    .name {
        position: relative;
        top:-55px;
        left:0%;
        

    }
    .delete {
        position: relative;
        top:75%;
        left:92%

    }

    .hist_input {
        position: relative;
        top:-45px;
        left:0%;
        background-color:rgb(243, 243, 243) ;
        border-radius: 4px;
        padding-left: 4px;
        padding-right: 4px;
    }
    .Card {    
        content: '';
		background-color: #ff3e00;
		border-radius: 30px;
		box-shadow: 0 2px 4px rgba(0,0,0,0.2);
		height: 40px;
        width: 40px;
		position: relative;
        left:90%;
        top:-35px;
	}

    p.test {
        font-size: 1.5em;
        font-weight: 400;
        color: white;
        padding-top:0px;
        text-align: center;
    
    }
</style>

