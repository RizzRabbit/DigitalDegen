<script lang="ts">
    import { getGameService } from '../game/context';
    import { t } from '@lingui/macro';
    import SymbolSprite from './SymbolSprite.svelte';
    import { getSymbolInfo } from '../game/utils';
    import { SYMBOL_INFO_MAP, SYMBOL_SIZE } from '../game/constants';

    const gameService = getGameService();

    function closePaytable() {
        gameService.send('CLOSE_PAYTABLE');
    }

    const symbols = Object.keys(SYMBOL_INFO_MAP);
</script>

<div class="paytable-screen">
    <h2>{t`Paytable`}</h2>
    <div class="symbols-container">
        {#each symbols as symbolName}
            <div class="symbol-item">
                <SymbolSprite symbolInfo={getSymbolInfo({ rawSymbol: { name: symbolName }, state: 'static' })} />
                <p>{symbolName}: Payouts vary</p>
            </div>
        {/each}
    </div>
    <p>This is where the paytable information will go. We will display symbol payouts here.</p>
    <button on:click={closePaytable}>{t`Close`}</button>
</div>

<style>
    .paytable-screen {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: rgba(0, 0, 0, 0.8);
        color: white;
        padding: 20px;
        border-radius: 10px;
        z-index: 1000;
        text-align: center;
        max-height: 80%;
        overflow-y: auto;
    }

    .symbols-container {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 20px;
        margin-top: 20px;
    }

    .symbol-item {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    button {
        margin-top: 20px;
        padding: 10px 20px;
        background-color: #007bff;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }
</style>
