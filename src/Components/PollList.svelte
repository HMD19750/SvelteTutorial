<script>
   // import {onMount,onDestroy} from "svelte";
    import PollStore from "../Stores/PollStore.js"
    import PollDetail from "./PollDetail.svelte";
 
    //export let polls=[];

/*     const unsub=PollStore.subscribe((data)=>{
        polls=data;
    }); */

    /* // Voor demo doeleinden een onMount functie
    onMount(()=>{
        console.log('Component mounted');
    });

    //Unsubscribe from store on destroy of component
    onDestroy(()=>{
        unsub();
    }); */
</script>

<div class="poll-list" >    <!-- Let op $ voor de naam van de store! --> 
    {#each $PollStore as poll (poll.id)}    
        <PollDetail poll={poll} />
    {/each}
</div>


<style>
    .poll-list{
        display:grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;
    }
</style>