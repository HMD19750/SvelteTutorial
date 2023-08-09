<script>
     import PollStore from "../Stores/PollStore.js"
     import Card from "../Shared/Card.svelte";
     import Button from "../Shared/Button.svelte";
     import {tweened} from "svelte/motion";

    export let poll;

    // Reactive values
    $: votes=poll.votesA+poll.votesB;
    $: percentA=Math.floor(100/votes*poll.votesA)||0; // De nul is om te voorkomen dat waarde onbepaald is bij creeren nieuwe poll
    $: percentB=Math.floor(100/votes*poll.votesB)||0;

    // Tweened percentages
    const tweenedA=tweened(0);
    const tweenedB=tweened(0);

    $: tweenedA.set(percentA);
    $: tweenedB.set(percentB);


    const handleVote=(option,id)=> {
        PollStore.update(currentPolls => {
            let copiedPolls=[...currentPolls];
            let upvotedPoll=copiedPolls.find((poll)=>poll.id==id);

            if(option==='a') {
                upvotedPoll.votesA++;
            } else if (option==='b') {
                upvotedPoll.votesB++;
            }

            return copiedPolls;
            })
	}

    // deleting a poll
    const handleDelete = (id) => {
        console.log("Delete poll");
        PollStore.update(polls => {
        return polls.filter(poll => poll.id != id);
        });
    };
</script>

<Card>
    <div class="poll">
        <h3>{poll.question}</h3>
        <p>Total votes: {votes}</p>
        <div class="answer" on:click={()=>handleVote('a',poll.id)}>
            <div class="percent percent-a" style="width:{$tweenedA}%">
            </div>
            <span>
                {poll.answerA} ({ poll.votesA })
            </span>
        </div>
        <div class="answer" on:click={()=>handleVote('b',poll.id)}>
            <div class="percent percent-b" style="width:{$tweenedB}%">
            </div>
            <span>
                {poll.answerB} ({ poll.votesB })
            </span>
        </div>
    </div>
    <div class="delete">
        <Button flat={true} on:click={() => handleDelete(poll.id)}>Delete</Button>
      </div>
   </Card>

<style>
h3{
    margin: 0 auto;
    color: #555;
}

p {
    margin-top: 6px;
    font-size: 14px;
    color:#aaa;
    margin-bottom: 30px;
}

.answer {
    background: #fafafa;
    cursor: pointer;
    margin: 10px auto;
    position: relative;
}

.answer:hover {
    opacity:0.6;
}

span {
    display: inline-block;
    padding: 10px 20px;
}

.percent {
    height:100%;
    position:absolute;
    box-sizing: border-box;
}

.percent-a {
    background:rgba(217,27,68,0.2);
    border-left: 4px solid #d91b42;
}

.percent-b {
    background:rgba(69,196,150,0.2);
    border-left: 4px solid #45c496;
}

.delete {
    margin-top:30px;
    text-align: center;
}
</style>