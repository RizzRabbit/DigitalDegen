<script lang="ts">
	import { getGameService } from '../game/context';
	import { stateBet, stateBetDerived } from 'state-shared';
	import { stateForceDerived } from 'state-shared/force';
	import { stateModal } from 'state-shared/modal';

	import { BetButton } from 'components-ui-html';
	import { InfoButton } from 'components-ui-html';
	import { PlayButton } from 'components-ui-html';
	import { AutoPlayButton } from 'components-ui-html';
	import { MaxBetButton } from 'components-ui-html';
	import { BetAmount } from 'components-ui-html';
	import { Balance } from 'components-ui-html';
	import { WinAmount } from 'components-ui-html';
	import { ForceBet } from 'components-ui-html';
	import { Modal } from 'components-ui-html';
	import { AutoSpinsCounter } from 'components-ui-html';
	import { BetMode } from 'components-ui-html';
	import { BetModeSelector } from 'components-ui-html';
	import { BetModeSelectorButton } from 'components-ui-html';
	import { BetModeSelectorDropdown } from 'components-ui-html';
	import { BetModeSelectorDropdownItem } from 'components-ui-html';
	import { BetModeSelectorDropdownItemText } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValue } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueText } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueTextValue } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueTextValueText } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueTextValueTextValue } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueTextValueTextValueText } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueTextValueTextValueTextValue } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueTextValueTextValueTextValueText } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueTextValueTextValueTextValueTextValueText } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueTextValueTextValueTextValueTextValueTextValueText } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueTextValueTextValueTextValueTextValueTextValueTextValueTextValue } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValue } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValue } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValue } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValue } from 'components-ui-html';
	import { BetModeSelectorDropdownItemValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValueTextValue } from 'components-ui-html';

	import PaytableScreen from './PaytableScreen.svelte';
	import InfoScreen from './InfoScreen.svelte';

	const gameService = getGameService();

	$: state = gameService.state.value;
	$: console.log('Current game state:', state); // Added console.log

	function onPlay() {
		console.log('Play button clicked. Sending SHOW_PAYTABLE event.'); // Added console.log
		gameService.send('SHOW_PAYTABLE'); // Changed to show paytable
	}

	function onAutoPlay() {
		gameService.send('AUTO_BET');
	}

	function onMaxBet() {
		stateBet.betAmount = stateBetDerived.maxBetAmount();
	}

	function onInfo() {
		console.log('Info button clicked. Sending SHOW_INFO event.'); // Added console.log
		gameService.send('SHOW_INFO'); // Changed to show info screen
	}

	function onBetModeChange(event: CustomEvent<string>) {
		stateBet.activeBetModeKey = event.detail;
	}

	function onBetAmountChange(event: CustomEvent<number>) {
		stateBet.betAmount = event.detail;
	}
</script>

<div class="game-ui">
	<div class="top-ui">
		<InfoButton on:click={onInfo} />
		<BetModeSelector
			activeBetModeKey={stateBet.activeBetModeKey}
			betModes={stateBet.betModes}
			on:change={onBetModeChange}
		/>
	</div>

	<div class="bottom-ui">
		<Balance balanceAmount={stateBet.balanceAmount} />
		<BetAmount
			betAmount={stateBet.betAmount}
			betAmounts={stateBetDerived.betAmounts()}
			on:change={onBetAmountChange}
		/>
		<MaxBetButton on:click={onMaxBet} />
		<PlayButton on:click={onPlay} />
		<AutoPlayButton on:click={onAutoPlay} autoSpinsCounter={stateBet.autoSpinsCounter} />
		<WinAmount winAmount={stateBet.winAmount} />
	</div>

	{#if stateForceDerived.force}
		<ForceBet />
	{/if}

	{#if stateModal.modal}
		<Modal modal={stateModal.modal} />
	{/if}

	{#if stateBet.autoSpinsCounter > 0}
		<AutoSpinsCounter autoSpinsCounter={stateBet.autoSpinsCounter} />
	{/if}

	{#if state === 'paytable'}
		<PaytableScreen />
	{/if}

	{#if state === 'info'}
		<InfoScreen />
	{/if}
</div>

<style>
	.game-ui {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		pointer-events: none; /* Allow clicks to pass through to the game */
	}

	.top-ui,
	.bottom-ui {
		display: flex;
		justify-content: space-around;
		width: 100%;
		pointer-events: all; /* Re-enable clicks for UI elements */
	}

	.top-ui {
		padding-top: 20px;
	}

	.bottom-ui {
		padding-bottom: 20px;
	}
</style>