<script>
    import Card from "../shared/Card.svelte";
    import { createEventDispatcher } from "svelte";
    import PollStore from "../stores/PollsStore.js";
    import Button from "../shared/Button.svelte";
    import {tweened} from "svelte/motion";

    export let poll;
    const dispatch = createEventDispatcher();

    //reactive values
    $: totalVotes = poll.votesA + poll.votesB;
    $: percentA = Math.floor(100/totalVotes*poll.votesA) || 0;
    $: percentB = Math.floor(100/totalVotes*poll.votesB) || 0;
    
    //tweened percentages
    const tweenedA = tweened(0);
    const tweenedB = tweened(0);

    $: tweenedA.set(percentA);
    $: tweenedB.set(percentB);

    const handleVote = (option,id)=>{

        PollStore.update(currentPolls=>{
            let copiedPolls = [...currentPolls];
		    let votedPoll = copiedPolls.find((poll)=> poll.id == id);

		    if (option ==='a'){
			    votedPoll.votesA++;
	    	}
		    if (option ==='b'){
			    votedPoll.votesB++;
		    }

		    return copiedPolls
        });
	
	}

    const handleDelete = (id)=>{
        PollStore.update(currentPolls=>{
            return currentPolls.filter(poll => poll.id != id);
        });
    }
</script>
<Card>
    <div class="poll">
        <h3>{poll.question}</h3>
        <p>Total Votes: {totalVotes}</p>
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <div class="answer" on:click={()=> handleVote('a', poll.id)}>
            <div class="percent percent-a" style="width:{$tweenedA}%"></div>
            <span>{poll.answerA} ({poll.votesA})</span>
        </div>
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <div class="answer" on:click={()=> handleVote('b', poll.id)}>
            <div class="percent percent-b" style="width:{$tweenedB}%"></div>
            <span>{poll.answerB} ({poll.votesB})</span>
        </div>
    </div>
    <div class="delete">
        <Button type="primary" on:click={()=> handleDelete(poll.id)}>Delete Poll</Button>
    </div>
    
</Card>

<style>
    h3{
        margin: 0 auto;
        color: #555;
    }

    p{
        margin-top: 6px;
        font-size: 14px;
        color: #aaa;
        margin-bottom: 30px;
    }

    .answer{
        background: #e8e6e6;
        cursor: pointer;
        margin: 10px auto;
        position: relative;
    }

    .answer:hover{
        opacity: 0.6;
    }
    span{
        display:inline-block;
        padding: 10px 20px;
    }

    .percent{
        height: 100%;
        position: absolute;
        box-sizing: border-box;
    }
    .percent-a{
        background:rgba(217,27,66,0.2);
    }
    .percent-b{
        background:rgba(69,169,150,0.2);
    }
    .delete{
        margin-top: 30px;
        text-align: center;
    }
</style>