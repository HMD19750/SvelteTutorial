<script>
    import {fade,slide,scale} from "svelte/transition";
    import {flip} from "svelte/animate";
    import PollStore from "../Stores/PollStore.js";
    import PollDetail from "./PollDetail.svelte";
    
 </script>

<div class="poll-list" >    <!-- Let op $ voor de naam van de store! --> 
    {#each $PollStore as poll (poll.id)}  
        <div in:fade out:scale|local animate:flip={{ duration:500 }}>  
            <PollDetail poll={poll} />
        </div>

    {/each}
</div>


<style>
    .poll-list{
        display:grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;
    }
</style>