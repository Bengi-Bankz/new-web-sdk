<script lang="ts">
	import type { Snippet } from 'svelte';

	import { Popup } from 'components-shared';
	import { zIndex } from 'constants-shared/zIndex';
	import { stateModal } from 'state-shared';

	import BaseContent from './BaseContent.svelte';
	import BaseScrollable from './BaseScrollable.svelte';

	type Props = {
		children: Snippet;
	};

	const props: Props = $props();
</script>

{#if stateModal.modal?.name === 'gameRules'}
	<Popup zIndex={zIndex.modal} onclose={() => (stateModal.modal = null)}>
		<BaseContent maxWidth="100%">
			<BaseScrollable type="column">
				<span>The normal mode of this game has a theoretical expected 
					 return of 97%.
The player also has the option to buy FREE SPINS.
 This costs 100x the underlying bet. The
FREE SPINS buy mode has a theoretical expected return of 97%.</span>
				{@render props.children()}
			</BaseScrollable>
		</BaseContent>
	</Popup>
{/if}
