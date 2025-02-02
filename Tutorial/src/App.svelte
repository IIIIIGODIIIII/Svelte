<!-- <script>
	let firstName = 'Harry';
	let lastName = 'Potter';
	let color = 'RED';

	// $: fullName = firstName + ' ' + lastName;
	$: fullName = `${firstName} ${lastName}`;

	// {} is used to run code inside the curly braces - Code block
	$: {
		console.log(color);
		console.log(fullName);
	}

	const darkLord = () => {
		firstname = 'Tom';
		lastname = '';
	}

	// Only required for 1 way binding
	const muggleText = (event) => {
		firstname = event.target.value;
		lastname = "";
	}
</script> -->

<!-- <main>
	<h1 style="color: {color}">{fullName} - {color}</h1>
	<input type="text" bind:value={firstName}>
	<input type="text" bind:value={lastName}>
	<input type="text" bind:value={color}>
</main> -->

<!-- <style>
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
</style> -->

<script>
    import Modal from './Modal.svelte';
	import AddWizardsForm from './AddWizardsForm.svelte';

	let showModal = false;

	let wizards = [
		{name: 'Harry Potter', house: 'Gryffindor', age: 17, id: 1},
		{name: 'Draco Malfoy', house: 'Slytherin', age: 17, id: 2},
		{name: 'Luna Lovegood', house: 'Ravenclaw', age: 16, id: 3},
		{name: 'Cedric Diggory', house: 'Hufflepuff', age: 17, id: 4},
	]

	const expelWizard = (id) => {
		// Remove the wizard from the array
		// Filter accepts a callback function that returns true or false
		wizards = wizards.filter((wizard) => wizard.id != id);
	}

	const sortingHat = () => {
		showModal = !showModal;
	}

	let age = 18;

	// The data passed to the event is the wizard object in the property called detail
	const addWizard = (wizard) => {
		console.log(wizard.detail);
		const newWizard = wizard.detail;
		// Add the new wizard to the array and keep the old wizards in the array, newWizard is the first element of the array
		wizards = [newWizard, ...wizards];	// wizards = [...wizards, newWizard] will add the new wizard to the end of the array
		showModal = false;
	}

</script>

<Modal isPromo = {true} {showModal} on:click={sortingHat}>
	<AddWizardsForm on:addWizard={addWizard}/>
</Modal>

<main>
	<button on:click|once={sortingHat}>Hogwarts School of Witchcraft and Wizardry</button>
	{#each wizards as wizard (wizard.id)}
		<div>
			<h4>{wizard.name}, Age - {wizard.age}</h4>

			{#if wizard.house == 'Gryffindor'}
				<p>Is a Gryffindor</p>
			{:else if wizard.house == 'Slytherin'}
				<p>Is a Slytherin</p>
			{:else if wizard.house == 'Ravenclaw'}
				<p>Is a Ravenclaw</p>
			{:else if wizard.house == 'Hufflepuff'}
				<p>Is a Hufflepuff</p>
			{/if}

			<button on:click={() => expelWizard(wizard.id)}>Expel Wizard</button>
		</div>

	{:else}
		<p>No wizards in the list you filthy muggle</p>
	{/each}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>