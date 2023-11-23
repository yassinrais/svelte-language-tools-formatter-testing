<script lang="ts">
	// example of file 
type ButtonSizes = 'small' | 'medium' | 'large';
type ButtonStyles = 'primary' | 'accent';

export let spinning = false;
export let reverse = false;
export let size: ButtonSizes = 'medium';
export let theme: ButtonStyles = 'primary';
</script>

<button
on:click
type="button"
class={['size--' + size, 'theme--' + theme].join(' ')}
class:reverse
class:spinning
{...$$props}
>
<slot />
</button>

<style lang="scss">
@use '../assets/mixin/reset';
@use '../assets/mixin/animations';

// Reset style
button {
	@include reset.button;

	--btn-color: var(--light);
	--btn-reverse-color: var(--primary);

	--btn-bg: var(--primary);
	--btn-border: var(--btn-bg);

	--btn-hover-bg: var(--light);

	color: var(--btn-color);
	padding: var(--padding);
	border-radius: var(--radius);

	background-color: var(--btn-bg);
	border: var(--btn-border) solid 2px;

	&::-moz-focus-inner {
		border: 0;
		padding: 0;
	}

	&[disabled] {
		opacity: var(--disabled-opacity, 0.4);
		pointer-events: none;
	}

	&.size {
		&--small {
			font-size: 0.8rem;
		}
		&--medium {
			font-size: 1rem;
		}
		&--large {
			font-size: 1.4rem;
		}
	}

	&.theme {
		&--primary {
			--btn-bg: var(--primary);
			--btn-reverse-color: var(--primary);

			&:hover {
				--btn-color: var(--primary);
			}
		}
		&--accent {
			--btn-bg: var(--accent);
			--btn-reverse-color: var(--accent);

			&:hover {
				--btn-color: var(--accent);
			}
		}
	}

	&:hover {
		--btn-bg: var(--btn-hover-bg);
		--btn-border: var(--btn-color);
	}

	&:focus {
		--btn-border: var(--btn-color);
	}

	&.reverse {
		--btn-bg: var(--btn-hover-bg);
		--btn-color: var(--btn-reverse-color);
		--btn-border: var(--btn-reverse-color);

		&:hover {
			--btn-bg: var(--btn-reverse-color);
			--btn-color: var(--light);
		}
	}
}

button {
	&.spinning {
		@include animations.circle-spinner(1rem, 2, var(--btn-color));
		color: transparent;
	}
}
</style>
