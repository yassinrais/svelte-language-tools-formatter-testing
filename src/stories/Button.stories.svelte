<script context="module">
	import '../app.scss';

	export const meta = {
		title: 'Button',
		component: Button,
	};
</script>

<script>
	import { Story, Template } from '@storybook/addon-svelte-csf';
	import Button from '../lib/components/Button.svelte';

	let disabled = false;
	function handleClick() {
		disabled = true;

		setTimeout(() => (disabled = false), 2000);
	}
</script>

<Template let:args>
	<!--👇 'on:click' allows to forward event to addon-actions  -->
	<Button
		{...args}
		disabled={disabled || args.disabled}
		spinning={disabled || args.spinning}
		on:click
		on:click={handleClick}>Button</Button
	>
</Template>

<Story
	name="Primary"
	args={{ theme: 'primary', disabled: false, spinning: false }}
/>
<Story
	name="Accent"
	args={{ theme: 'accent', disabled: false, spinning: false }}
/>
<Story
	name="Reversed"
	args={{
		theme: 'primary',
		disabled: false,
		spinning: false,
		reverse: true,
	}}
/>
