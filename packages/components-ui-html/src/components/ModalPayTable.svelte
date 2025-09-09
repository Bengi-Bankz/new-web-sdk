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

{#if stateModal.modal?.name === 'payTable'}
	<Popup zIndex={zIndex.modal} onclose={() => (stateModal.modal = null)}>
		<BaseContent maxWidth="100%">
			<BaseScrollable type="column" class="paytable-scrollable">
				<div class="paytable-modal">
						<h1 class="paytable-title">PAYTABLE</h1>
						<div class="paytable-section symbols">
							<h2 class="symbols-title">SYMBOLS</h2>
							<div class="symbols-grid">
								<!-- Example symbol row, repeat as needed -->
								<div class="symbol-item">
									<img src="/assets/symbol1.png" alt="Symbol 1" />
									<div>8-9 | 4x<br />10-11 | 5x<br />12+ | 10x</div>
								</div>
								<div class="symbol-item">
									<img src="/assets/symbol2.png" alt="Symbol 2" />
									<div>8-9 | 3x<br />10-11 | 4x<br />12+ | 8x</div>
								</div>
								<div class="symbol-item">
									<img src="/assets/symbol3.png" alt="Symbol 3" />
									<div>8-9 | 1x<br />10-11 | 2x<br />12+ | 4x</div>
								</div>
								<!-- Add more symbol items as needed -->
							</div>
						</div>
						<div class="paytable-version">production 2.5.0</div>
						{@render props.children()}
				</div>
			</BaseScrollable>
<style lang="scss">
.paytable-modal {
	color: #fff;
	font-family: 'Montserrat', Arial, sans-serif;
	padding: 0 0 32px 0;
	text-align: center;
	max-width: 900px;
	margin: 0 auto;
}
.paytable-title {
	font-size: 2.4rem;
	font-weight: 700;
	letter-spacing: 0.04em;
	margin: 0 0 36px 0;
	border-bottom: 1px solid rgba(255,255,255,0.12);
	padding-bottom: 12px;
}
.paytable-section {
	margin: 40px 0 0 0;
}
.paytable-row {
	display: flex;
	align-items: center;
	justify-content: center;
	gap: 48px;
	margin-bottom: 40px;
}
.paytable-row.single {
	flex-direction: column;
	gap: 0;
}
.paytable-icon {
	width: 120px;
	height: 120px;
	object-fit: contain;
	margin-right: 36px;
	filter: drop-shadow(0 2px 16px #0008);
}
.paytable-info {
	text-align: left;
	max-width: 520px;
	font-size: 1.15rem;
}
.paytable-info h2 {
	font-size: 1.5rem;
	font-weight: 700;
	margin: 0 0 12px 0;
	letter-spacing: 0.03em;
}
.paytable-info p {
	font-size: 1.15rem;
	margin: 0;
	line-height: 1.7;
}
.symbols {
	margin-top: 48px;
}
.symbols-title {
	font-size: 1.7rem;
	font-weight: 700;
	margin-bottom: 24px;
}
.symbols-grid {
	display: flex;
	flex-wrap: wrap;
	gap: 40px 56px;
	justify-content: center;
}
.symbol-item {
	display: flex;
	flex-direction: column;
	align-items: center;
	min-width: 140px;
	font-size: 1.1rem;
	background: rgba(30,34,44,0.7);
	border-radius: 16px;
	padding: 18px 12px 12px 12px;
	box-shadow: 0 2px 8px #0004;
}
.symbol-item img {
	width: 68px;
	height: 68px;
	margin-bottom: 10px;
}
.paytable-version {
	margin-top: 48px;
	font-size: 1.05rem;
	color: #aaa;
	opacity: 0.7;
}
@media (max-width: 900px) {
	.paytable-modal {
		padding: 0 8px 32px 8px;
	}
	.paytable-title {
		font-size: 2rem;
	}
	.paytable-info h2 {
		font-size: 1.2rem;
	}
	.symbols-title {
		font-size: 1.2rem;
	}
}
@media (max-width: 700px) {
	.paytable-row, .symbols-grid {
		flex-direction: column;
		gap: 24px;
	}
	.paytable-icon {
		margin-right: 0;
		margin-bottom: 18px;
		width: 80px;
		height: 80px;
	}
	.paytable-info {
		text-align: center;
		max-width: 100%;
		font-size: 1rem;
	}
	.symbol-item {
		min-width: 100px;
		font-size: 0.95rem;
		padding: 12px 6px 8px 6px;
	}
	.symbol-item img {
		width: 48px;
		height: 48px;
	}
}
@media (max-width: 500px) {
	.paytable-title {
		font-size: 1.3rem;
		padding-bottom: 6px;
	}
	.paytable-info h2 {
		font-size: 1rem;
	}
	.paytable-info p {
		font-size: 0.9rem;
	}
	.symbols-title {
		font-size: 1rem;
	}
	.paytable-modal {
		padding: 0 2px 16px 2px;
	}
}
/* Ensure the scrollable area works on all screens */
.paytable-scrollable {
	max-height: 80vh;
	overflow-y: auto;
}
</style>
		</BaseContent>
	</Popup>
{/if}
