<script lang="ts">
	type Props = {
		width: string;
		height: string;
		background?: string;
		border?: string;
	};

	const { width, height, background = 'white', border = 'white' }: Props = $props();
</script>


<div
	class="rectangle modern-icon"
	style="
		--width-value: {width};
		--height-value: {height};
		--background-value: {background};
		--border-value: {border};
	"
></div>

<!-- ADD YOUR DESIGN -->

<!-- <script lang="ts">
	import { sharedAssetsHtml as assets } from 'constants-shared/assets';

	type Icon = keyof typeof assets;

	type Props = {
		icon: Icon;
		hovered?: Icon;
		pressed?: Icon;
		size?: string;
		disabled?: boolean;
	};

	const { icon, hovered, pressed, size = '1rem', disabled = false }: Props = $props();

	const defaultUrl = $derived(assets[icon] as string);
	const hoveredUrl = $derived((hovered ? assets[hovered] : defaultUrl) as string);
	const pressedUrl = $derived((pressed ? assets[pressed] : defaultUrl) as string);

	let hoveredState = $state(false);
	let pressedState = $state(false);

	const src = $derived.by(() => {
		if (disabled) return defaultUrl;
		if (hoveredState) return hoveredUrl;
		if (pressedState) return pressedUrl;
		return defaultUrl;
	});
</script>

<div
	style="width: {size}; height: {size};"
	on:mouseenter={() => (hoveredState = true)}
	on:mouseleave={() => (hoveredState = false)}
	on:mousedown={() => (pressedState = true)}
	on:mouseup={() => (pressedState = false)}
	on:pointerdown={() => (pressedState = true)}
	on:pointerup={() => (pressedState = false)}
>
	<img {src} style="width: 100%; object-fit: cover;" alt={icon} />
</div> -->

<style lang="scss">
	.rectangle.modern-icon {
		width: var(--width-value);
		height: var(--height-value);
		/* Modern translucent black with baby blue/white accent */
		background: linear-gradient(135deg, rgba(30,34,44,0.85) 70%, rgba(137,207,240,0.25) 100%);
		border: 2px solid rgba(137,207,240,0.7); /* baby blue border */
		border-radius: 16px;
		box-shadow: 0 4px 24px 0 rgba(30,34,44,0.18), 0 1.5px 6px 0 rgba(137,207,240,0.10);
		display: flex;
		align-items: center;
		justify-content: center;
		transition: box-shadow 0.2s, border-color 0.2s, background 0.2s;
		position: relative;
		overflow: hidden;
	}
	.rectangle.modern-icon::after {
		content: '';
		position: absolute;
		inset: 0;
		border-radius: 16px;
		pointer-events: none;
		box-shadow: 0 0 0 1.5px rgba(255,255,255,0.08) inset;
	}
	.rectangle.modern-icon:hover {
		border-color: #89cff0;
		box-shadow: 0 6px 32px 0 rgba(137,207,240,0.18), 0 2px 8px 0 rgba(137,207,240,0.18);
		background: linear-gradient(135deg, rgba(30,34,44,0.92) 60%, rgba(137,207,240,0.35) 100%);
	}
</style>
