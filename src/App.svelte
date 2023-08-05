<script>
	import Modal from './Modal.svelte'

	let showModal=false;

	let people=[
		{name: "Hubert", age:66, beltColor:"green", id:1},
		{name: "Rens", age:35, beltColor:"white", id:2},
		{name: "Camiel", age:33, beltColor:"black", id:3}
	]

	const clickHandler=(id)=>{
		people=people.filter((person)=>person.id!=id)
		console.log(id + "deleted")
	}

	const toggleModal= () => {
		showModal=!showModal;
	}
</script>

<Modal message="Hi, I am a prop value!" isPromo={false} showModal={showModal} on:click={toggleModal}/>
<main>

	<button on:click={toggleModal}>Open Modal</button>

	{#each people as person (person.id) }
		<div>
			<h4 style="color:{person.beltColor}">{person.name}</h4>
			{#if person.beltColor==="black"}
				<p><strong>Master Ninja</strong></p>
			{/if}
			<p>{person.age} years old, {person.beltColor} belt</p>
			<button on:click={()=>clickHandler(person.id)}>Delete</button>
		</div>
	{:else}
		<p>There are no people to show</p>
	{/each}

</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>