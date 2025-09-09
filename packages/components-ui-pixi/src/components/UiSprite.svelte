<script lang="ts" module>
	import { Rectangle, type RectangleProps } from 'pixi-svelte';

	export type Props = RectangleProps;
</script>

<script lang="ts">
	const props: Props = $props();
</script>


<Rectangle
	borderRadius={50}
	fill={0x0a192f}
	lineColor={0xb3e0ff}
	lineWidth={6}
	filters={[
		{
			distance: 16,
			outerStrength: 2,
			innerStrength: 0.5,
			quality: 0.5
		}
	]}
	{...props}
/>

<!-- PIXI 'Starlight' style: deep black fill, baby blue border, and glow filter. -->

<!-- ADD YOUR DESIGN -->

<!-- <script lang="ts" module>
	import { Sprite, type SpriteProps } from 'pixi-svelte';
	import type { sharedAssetsPixi } from 'constants-shared/assets';

	export type Props = SpriteProps & {
		key: keyof typeof sharedAssetsPixi;
	};
</script>

<script lang="ts">
	const props: Props = $props();
</script>

<Sprite {...props} /> -->
