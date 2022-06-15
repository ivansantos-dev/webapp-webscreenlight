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
	};

	const changeBackgroundColor = () => {
		document.body.style.backgroundColor = color;
	};
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
