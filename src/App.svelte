<script>

  	let questions = [
		{ id: 1, text: `Donut` },
		{ id: 2, text: 'Rectangle' },
		{ id: 3, text: 'Cone' }
	];

  let selected;

	let answer = '';


  let selectedMaterial 
  let materials 
  let selectedColor
  let Colors
  let Check 

  $: if (selectedPrinter == 'Prusa MK3') {
    selectedMaterial = 'PLA'
		materials = ['ABS','TPU','PLA', 'PETG','PLA+'];
	  }
    else if (selectedPrinter == 'Prusa MK2'){
    selectedMaterial = 'ABS'
    materials = ['ABS','TPU'];
    }


  $: if (selectedPrinter == 'Prusa MK3') {
    selectedColor = 'Black'
    Colors = ['Black','White','Red', 'Blue','Orange'];
	  }
    else if (selectedPrinter == 'Prusa MK2'){
    selectedColor = ''
    Colors = ['Red', 'Blue','Orange'];
    }


  let selectedPrinter = 'Prusa MK3'
  let Printers = ['Prusa MK3','Prusa MK2']


  $:if (selected == "") {
      Check = true;
    } else if (selectedPrinter == "") {
      Check = true;
    } else if (selectedMaterial == "") {
      Check = true;
    } else if (selectedColor == "") {
      Check = true;
    } else {
      Check =  false;
    }

</script>

<h1>Welcome</h1>



<h2>Objekt</h2>
  <select bind:value={selected} on:change={() => (answer = ' ')}>
    {#each questions as question}
      <option value={question}>
        {question.text}
      </option>
    {/each}
  </select>

<h2>Printer</h2>

{#each Printers as printer}
	<label>
		<input type="radio" bind:group={selectedPrinter} value={printer} />
		{printer}
	</label>
{/each}

<h2>Material</h2>

{#each materials as material}
	<label>
		<input type="radio" bind:group={selectedMaterial} value={material} />
		{material}
	</label>
{/each}


<h2>Colors</h2>
{#each Colors as color}
	<label>
		<input type="radio" bind:group={selectedColor} value={color} />
		{color}
	</label>
{/each}
<p>
	You ordered a {selectedColor} {selected ? selected.text : '[waiting...]'} in {selectedMaterial} 
</p>
<button disabled={Check}> Order </button>
