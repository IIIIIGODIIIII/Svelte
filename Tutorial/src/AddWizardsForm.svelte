<script>
    import {createEventDispatcher} from 'svelte';

    let dispatch = createEventDispatcher();

    let name;
    let house;
    let age;

    // Grouping attributes
    let skills = {
        magic: false,
        charm: false,
        stealth: false
    }

    const addWizard = () => {
        console.log(name, house, age, skills);
        const wizard = {
            name: name,
            house: house,
            age: age,
            skills: skills,
            id: Math.random()
        }
        // addWizard is the name of the event that will be dispatched, and wizard is the data that will be passed to the event
        dispatch('addWizard', wizard);
    }

</script>

<form on:submit|preventDefault = {addWizard}>
    <input type="text" placeholder="Name" bind:value={name}>
    <input type="number" placeholder="Age" bind:value={age}>

    <label>Skills:</label>
    <input type="checkbox" bind:checked={skills.magic}> Magic <br>
    <input type="checkbox" bind:checked={skills.charm}> Charm <br>
    <input type="checkbox" bind:checked={skills.stealth}> Stealth <br>

    <label>House:</label>
    <select bind:value={house}>
        <option value="Gryffindor">Gryffindor</option>
        <option value="Slytherin">Slytherin</option>
        <option value="Hufflepuff">Hufflepuff</option>
        <option value="Ravenclaw">Ravenclaw</option>
    </select>

    <button>Add Wizard</button>
</form>

<style>

</style>