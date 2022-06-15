<script lang="ts">
	let color = '#FFFFFF';
	let presetColor: string;

	const presetColors = [
		{
			name: 'white',
			hex: '#FFFFFF'
		},
		{
			name: 'black',
			hex: '#000000'
		},
		{
			name: 'warm white',
			hex: '#FDF4DC'
		},
		{
			name: 'daylight',
			hex: '#F4E99B'
		},
		{
			name: 'cool white',
			hex: '#F4FDFF'
		}
	];

	const selectPresetColor = () => {
		document.body.style.backgroundColor = presetColor;
		color = presetColor;
		document.body.style.color = contrast(color);
	};

	const contrast = (hexcolor: string) => {
		hexcolor = hexcolor.slice(1);
		const r = parseInt(hexcolor.slice(0, 2), 16);
		const g = parseInt(hexcolor.slice(2, 4), 16);
		const b = parseInt(hexcolor.slice(4, 6), 16);
		const yiq = r * 0.299 + g * 0.587 + b * 0.114;
		console.log(hexcolor, r, g, b, yiq);
		return yiq > 186 ? 'black' : 'white';
	};

	const changeBackgroundColor = () => {
		document.body.style.backgroundColor = color;
		document.body.style.color = contrast(color);
	};

	// function to find contrast of hex color
</script>

<svelte:head>
	<title>Web Screen Light | Online Tool</title>
</svelte:head>

<div class="row mb-3">
	<div class="col-sm-2">
		<label for="colorPreset" class="col-form-label">Color Presets</label>
	</div>
	<div class="col-sm-2">
		<select
			name="colorPreset"
			id="colorPreset"
			bind:value={presetColor}
			on:change={selectPresetColor}
			class="form-select mb-3"
		>
			{#each presetColors as color}
				<option value={color.hex}>
					{color.name}
				</option>
			{/each}
		</select>
	</div>
</div>

<label for="color" class="col-sm-2 col-form-label">Color Picker</label>
<input type="color" name="color" id="color" bind:value={color} on:input={changeBackgroundColor} />
