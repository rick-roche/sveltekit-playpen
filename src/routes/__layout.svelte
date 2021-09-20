<script lang="ts">
	import TopAppBar, {
		Row,
		Section,
		Title,
		AutoAdjust,
		TopAppBarComponentDev
	} from '@smui/top-app-bar';
	import IconButton, { Icon } from '@smui/icon-button';
	// import Button, { Label } from '@smui/button';
	import { Svg } from '@smui/common/elements';
	import LayoutGrid, { Cell } from '@smui/layout-grid';

	import { mdiGithub, mdiTwitter, mdiWeb } from '@mdi/js';

	let dense = true;
	let prominent = false;
	let variant = 'fixed';
	let title = 'Title';
	let topAppBar: TopAppBarComponentDev;

	let lightTheme =
		typeof window === 'undefined' || window.matchMedia('(prefers-color-scheme: light)').matches;
	function switchTheme() {
		lightTheme = !lightTheme;
		let themeLink = document.head.querySelector<HTMLLinkElement>('#theme');
		if (!themeLink) {
			themeLink = document.createElement('link');
			themeLink.rel = 'stylesheet';
			themeLink.id = 'theme';
		}
		themeLink.href = `/smui${lightTheme ? '' : '-dark'}.css`;
		document.head
			.querySelector<HTMLLinkElement>('link[href="/smui-dark.css"]')
			?.insertAdjacentElement('afterend', themeLink);
	}
</script>

<TopAppBar bind:this={topAppBar} {dense} {prominent} {variant} color="secondary">
	<Row>
		<Section>
			<Title>{title}</Title>
		</Section>
		<Section align="end" toolbar>
			<IconButton href="http://www.rickroche.com" target="_blank">
				<Icon component={Svg} viewBox="0 0 24 24">
					<path fill="currentColor" d={mdiWeb} />
				</Icon>
			</IconButton>
			<IconButton href="https://twitter.com/rickroche_" target="_blank">
				<Icon component={Svg} viewBox="0 0 24 24">
					<path fill="currentColor" d={mdiTwitter} />
				</Icon>
			</IconButton>
			<IconButton href="https://github.com/rick-roche" target="_blank">
				<Icon component={Svg} viewBox="0 0 24 24">
					<path fill="currentColor" d={mdiGithub} />
				</Icon>
			</IconButton>
			<IconButton on:click={switchTheme} bind:pressed={lightTheme}>
				<Icon class="material-icons">light_mode</Icon>
				<Icon class="material-icons" on>dark_mode</Icon>
			</IconButton>
		</Section>
	</Row>
</TopAppBar>
<AutoAdjust {topAppBar} />

<div style="display: flex; justify-content: space-between;">
	<LayoutGrid>
		<Cell>
			<div class="demo-cell"><slot /></div>
		</Cell>
	</LayoutGrid>
</div>

<style>
	/* Hide everything above this component. */
	:global(app),
	:global(body),
	:global(html) {
		display: block !important;
		height: auto !important;
		width: auto !important;
		position: static !important;
		margin: 0px;
	}
</style>
