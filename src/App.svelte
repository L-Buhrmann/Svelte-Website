<script>
  import test from './assets/pencils-452238_640.jpg';
  import logo from "./assets/ostfalia-logo-removebg-preview.png"
  let imglogo = logo
  let questions = [ `Donut` , 'Rectangle' , 'Cone' ,'Custom Upload' ];

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
    Colors = [
		{ color: 'Black', image: `https://via.placeholder.com/40x60/0bf/fff&text=A` },
		{ color: 'White', image: 'https://via.placeholder.com/40x60/b0f/fff&text=B' },
		{ color: 'Red', image: 'https://via.placeholder.com/40x60/0bf/fff&text=A' },
    { color: 'Blue', image: 'https://via.placeholder.com/40x60/b0f/fff&text=B' },
    { color: 'Orange', image: 'https://via.placeholder.com/40x60/0bf/fff&text=A' }
	];
	  }
    else if (selectedPrinter == 'Prusa MK2'){
    selectedColor = ''
    Colors = [
      { color: 'Red', image: logo },
      { color: 'Blue', image: 'https://via.placeholder.com/40x60/b0f/fff&text=B' },
      { color: 'Orange', image: 'https://via.placeholder.com/40x60/0bf/fff&text=A' }
    ];
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
  
let files;

$: if (files) {
  // Note that `files` is of type `FileList`, not an Array:
  // https://developer.mozilla.org/en-US/docs/Web/API/FileList
  console.log(files);

  for (const file of files) {
    console.log(`${file.name}: ${file.size} bytes`);
  }
}

</script>



  <h1 style= float:left >Welcome</h1>
  <img style= float:right;  src = {imglogo} alt = "Logo Ostfalia"/> 
  <h2 style= clear:both >Object</h2>
    <select class="selectbox" bind:value={selected} on:change={() => (answer = ' ')}>
      {#each questions as question}
        <option value={question}>
          {question}
        </option>
      {/each}
    </select>
    {#if selected == "Custom Upload" }
      <label for="avatar">Upload your GCode file:</label>
      <input accept="gcode" bind:files id="avatar" name="avatar" type="file" />
    {/if}

  <h2>Printer</h2>

  {#each Printers as printer}
    <label>
      <input type="radio" bind:group={selectedPrinter} value={printer} />
      {printer}
    </label>
  {/each}

  <h2 class="testOutline">Material</h2>

  {#each materials as material}
    <label class="testOutline">
      <input type="radio" bind:group={selectedMaterial} value={material} />
      {material}
    </label>
  {/each}


  <h2 class="testOutline">Colors</h2>
  {#each Colors as color}
    <label class="colors">
      <input class="radiocolors" type="radio" bind:group={selectedColor} value={color.color}  />
      <figure class="figurecolors">
        
        <img class="imagecolors" src={color.image} alt="Test" />
        <figcaption>{color.color}</figcaption>
      </figure >
    </label>
  {/each}

  <label class="submit">
    <h2 class="testOutline">Summary </h2>
    <p class="submittext">
    You ordered a {selectedColor} {selected} in {selectedMaterial} 
    </p>
  <button disabled={Check}> Order </button>
  </label>


<style>
  .testOutline{
    /*outline: solid #ff004a;*/
  }

  .selectbox {
	cursor: pointer;
	outline:0;
	color: #333333;
	font-size: 20px;
	padding: 10px 10px;
	min-width: 304px;
	font-weight: bold;
	border-radius: 8px;
	border: 2px solid #D0C1D6FF;
	background-color:rgb(149, 216, 236);
}
.selectbox:hover, .selectbox:focus {
	background-color: #FFCD58FF;
	color: #000000;
	border: 2px solid #969696;
}


  .colors{
    float:left;
    top: 0;
    display: flex;
    height: 100px;
    margin-top: -5px;
    /*outline: solid #ff004a;*/
  }
  .figurecolors{
    height: 70px;
    width: 100px;
    text-align: center;
    top: 0;
    display:center;
    margin: 15px;
    margin-top: 2px;
    /*outline: solid #ff004a;*/
  }
  .imagecolors{
    float:center;
    max-width:100%;
  }
  .radiocolors{
    position: center;
    opacity: 0;
    width: 0;
    height: 0;
  }
  .radiocolors +  .figurecolors .imagecolors {
  cursor: pointer;
  }
  .radiocolors:checked +  .figurecolors .imagecolors{
    background: radial-gradient(circle at 100% 100%, #ffffff 0, #ffffff 3px, transparent 3px) 0% 0%/7px 7px no-repeat,
            radial-gradient(circle at 0 100%, #ffffff 0, #ffffff 3px, transparent 3px) 100% 0%/7px 7px no-repeat,
            radial-gradient(circle at 100% 0, #ffffff 0, #ffffff 3px, transparent 3px) 0% 100%/7px 7px no-repeat,
            radial-gradient(circle at 0 0, #ffffff 0, #ffffff 3px, transparent 3px) 100% 100%/7px 7px no-repeat,
            linear-gradient(#ffffff, #ffffff) 50% 50%/calc(100% - 8px) calc(100% - 14px) no-repeat,
            linear-gradient(#ffffff, #ffffff) 50% 50%/calc(100% - 14px) calc(100% - 8px) no-repeat,
            linear-gradient(36deg, #ff004a 0%, #34478b 100%);
    border-radius: 3px;
    padding: 3px;
    box-sizing: border-box;


  } 
  .submit{
    clear:both;
    float:center;
    display: block;
    position: relative;
    /*outline: solid #ff004a;*/
    }
  .submittext{
    /*outline: solid #ff004a;*/
    margin-top: -5px;
  }

  :root {
	--font-body: Arial, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu,
		Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
	--font-mono: 'Fira Mono', monospace;
	--color-bg-0: rgb(202, 216, 228);
	--color-bg-1: hsl(209, 36%, 86%);
	--color-bg-2: hsl(224, 44%, 95%);
	--color-theme-1: #ff3e00;
	--color-theme-2: #4075a6;
	--color-text: rgba(0, 0, 0, 0.7);
	--column-width: 42rem;
	--column-margin-top: 4rem;
	font-family: var(--font-body);
	color: var(--color-text);
  }
  
  
</style>
