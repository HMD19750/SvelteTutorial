<script>
	import Header from "./Components/Header.svelte"
	import Footer from "./Components/Footer.svelte"
	import Tabs from "./Shared/Tabs.svelte"
  	import CreatePollForm from "./Components/CreatePollForm.svelte";
	import PollList from "./Components/PollList.svelte";

	//Tabs
	let items=['Current Polls', 'Add new Poll'];
	let activeItem="Current Polls";
	
	const tabChange=(e) => {
		activeItem=e.detail;
	}

	const handleAdd=()=>{
		activeItem="Current Polls";
	}

</script>

<Header />
<main>
	<Tabs items={items}  activeItem={activeItem} on:tabChange={tabChange}/>
	
	{#if activeItem==="Current Polls"}
		<PollList />
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