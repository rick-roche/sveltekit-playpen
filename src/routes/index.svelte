<script lang="ts">
	import { mdiSpotify } from '@mdi/js';

	import Radio from '@smui/radio';
	import FormField from '@smui/form-field';
	import Button, { Label, Icon } from '@smui/button';
	// import IconButton, { Icon } from '@smui/icon-button';
	import { Svg } from '@smui/common/elements';
	import Select, { Option } from '@smui/select';
	import Textfield from '@smui/textfield';
	import HelperText from '@smui/textfield/helper-text/index';
	import TFIcon from '@smui/textfield/icon';

	let options = [
		{
			name: 'Disabled',
			value: 'disabled',
			disabled: true
		},
		{
			name: 'Active',
			value: 'active',
			disabled: false
		}
	];
	let selected = 'active';

	let clicked = 0;

	let selectTypes = [
		{ name: 'Type A', value: 'type-a' },
		{ name: 'Type B', value: 'type-b' }
	];

	let selectedType = '';
	let username = '';
	let toDate = '';
	let fromDate = '';
	let limit = 100;
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<div class="button-demo">
	<Button on:click={() => clicked++} touch variant="raised" href="http://localhost:8080/v1/auth">
		<!-- <Icon class="material-icons">mdiSpotify</Icon> -->
		<Icon component={Svg} viewBox="0 0 24 24">
			<path fill="currentColor" d={mdiSpotify} />
		</Icon>
		<Label>Login to Spotify</Label>
	</Button>

	<pre class="status">Clicked: {clicked}</pre>
</div>

<div class="radio-demo">
	{#each options as option}
		<FormField>
			<Radio bind:group={selected} value={option.value} disabled={option.disabled} />
			<span slot="label">
				<!-- {option.name}{option.disabled ? ' (disabled)' : ''} -->
				{option.name}
			</span>
		</FormField>
	{/each}
	<pre class="status">Selected service: {selected}</pre>
</div>

<p />
<div class="dropdown-demo">
	<div>
		<Select variant="outlined" bind:value={selectedType} label="Types">
			{#each selectTypes as st}
				<Option value={st.value}>{st.name}</Option>
			{/each}
		</Select>

		<pre class="status">Selected: {selectedType}</pre>
	</div>
</div>

<p />
<div class="input-demo">
	<div>
		<Textfield variant="outlined" bind:value={username} label="Leading Icon">
			<TFIcon class="material-icons" slot="leadingIcon">account_circle</TFIcon>
			<HelperText slot="helper">Helper Text</HelperText>
		</Textfield>

		<pre class="status">Value: {username}</pre>
	</div>

	<div>
		<!-- <Textfield bind:value={toDate} label="To Date" type="month" /> -->
		<Textfield bind:value={toDate} label="To Date" type="date" />
		<Textfield bind:value={fromDate} label="From Date" type="date" />

		<pre class="status">To: {toDate}</pre>
		<pre class="status">From: {fromDate}</pre>
	</div>

	<div>
		<Textfield bind:value={limit} label="Limit" type="number" />
		<pre class="status">Limit: {limit}</pre>
	</div>
</div>
