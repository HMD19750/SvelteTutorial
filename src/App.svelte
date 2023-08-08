<script>
	import Header from "./Components/Header.svelte"
	import Footer from "./Components/Footer.svelte"
	import Tabs from "./Shared/Tabs.svelte"
  	import CreatePollForm from "./Components/CreatePollForm.svelte";
	import PollList from "./Components/PollList.svelte";

	//Tabs
	let items=['Current Polls', 'Add new Poll'];
	let activeItem="Current Polls";

	// Polls
	let polls=[
		{
			id:1,
			question: "Python or Javascript",
			answerA: 'Python',
			answerB: 'Javascript',
			votesA: 9,
			votesB: 15
		},
	];

	const tabChange=(e) => {
		activeItem=e.detail;
	}

	const handleAdd=(e)=>{
		const poll=e.detail;
		polls=[poll,...polls];
		activeItem="Current Polls";
	}

	const handleVote=(e)=> {
		const {id,option}=e.detail;

		let copiedPolls=[...polls];
		let upvotedPoll=copiedPolls.find((poll)=>poll.id==id);

		if(option==='a') {
			upvotedPoll.votesA++;
		} else if (option==='b') {
			upvotedPoll.votesB++;
		}

		polls=copiedPolls;

	}
</script>

<Header />
<main>
	<Tabs items={items}  activeItem={activeItem} on:tabChange={tabChange}/>
	
	{#if activeItem==="Current Polls"}
		<PollList polls={polls} on:vote={handleVote}/>
	{:else if activeItem==="Add new Poll"}
		<CreatePollForm on:add={handleAdd}/>
	{/if}
</main>
<Footer />

<style>
main {
	max-width: 960px;
	margin: 20px auto;
}
</style>